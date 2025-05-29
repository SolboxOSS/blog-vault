다음은 현재 Docusaurus에 적용된 JavaScript 기반의 이미지 확대 기능을 **GLightbox**로 교체하고, **동영상 확대** 기능까지 추가하는 가장 깔끔한 방법입니다.

---

## **🚀 1단계: GLightbox 설치하기**

  

먼저 GLightbox를 npm으로 설치합니다.

```
npm install glightbox
```

  

---

## **🛠️ 2단계: Docusaurus 프로젝트에 GLightbox 초기화하기**

  

다음 위치에 **GLightbox** 초기화 코드를 추가합니다.

- 파일 경로: src/theme/Root.js

두번확대 제거 및 확대된 이미지의 바깥 영역을 누를때 창을 닫는 방식
```
import React, { useEffect } from 'react';
import { useLocation } from '@docusaurus/router';

export default function Root({ children }) {
  const location = useLocation();

  useEffect(() => {
    if (typeof window !== 'undefined') {
      Promise.all([
        import('glightbox').then((mod) => mod.default),
        import('glightbox/dist/css/glightbox.min.css'),
      ]).then(([GLightbox]) => {
        const initializeGlightbox = () => {
          const mediaElements = document.querySelectorAll(".theme-doc-markdown img, .theme-doc-markdown video");

          mediaElements.forEach(media => {
            if (!media.closest('a.glightbox')) {
              const wrapper = document.createElement('a');
              const src = media.tagName.toLowerCase() === 'video'
                ? media.querySelector('source').src
                : media.src;
              wrapper.href = src;
              wrapper.classList.add('glightbox');
              media.parentNode.insertBefore(wrapper, media);
              wrapper.appendChild(media);
            }
          });

          if (window.lightboxInstance) {
            window.lightboxInstance.destroy();
          }

          window.lightboxInstance = GLightbox({
            selector: '.glightbox',
            loop: true,
            autoplayVideos: true,
            zoomable: false, // ← 확대 2번 기능 끄기
          });
        };

        initializeGlightbox();
      });
    }
  }, [location.pathname]);

  return <>{children}</>;
}
```

확대된 이미지 클릭시, 창 닫는 방식
```
import React, { useEffect } from 'react';
import { useLocation } from '@docusaurus/router';

export default function Root({ children }) {
  const location = useLocation();

  useEffect(() => {
    if (typeof window !== 'undefined') {
      Promise.all([
        import('glightbox').then((mod) => mod.default),
        import('glightbox/dist/css/glightbox.min.css'),
      ]).then(([GLightbox]) => {
        const initializeGlightbox = () => {
          const mediaElements = document.querySelectorAll(".theme-doc-markdown img, .theme-doc-markdown video");

          mediaElements.forEach(media => {
            if (!media.closest('a.glightbox')) {
              const wrapper = document.createElement('a');
              const src = media.tagName.toLowerCase() === 'video'
                ? media.querySelector('source').src
                : media.src;
              wrapper.href = src;
              wrapper.classList.add('glightbox');
              media.parentNode.insertBefore(wrapper, media);
              wrapper.appendChild(media);
            }
          });

          if (window.lightboxInstance) {
            window.lightboxInstance.destroy();
          }

          window.lightboxInstance = GLightbox({
            selector: '.glightbox',
            loop: true,
            autoplayVideos: true,
            zoomable: false,
            closeOnSlideClick: true,
          });

          window.lightboxInstance.on('open', () => {
            const container = document.querySelector('.gcontainer');

            if (container) {
              container.addEventListener('click', function(event) {
                const image = event.target.closest('.gslide-image img');
                if (image) {
                  window.lightboxInstance.close();
                }
              });
            }
          });
        };

        initializeGlightbox();
      });
    }
  }, [location.pathname]);

  return <>{children}</>;
}
```

위의 설정은 .theme-doc-markdown 영역 내의 모든 요소 중 .glightbox 클래스를 가진 미디어를 클릭 시 확대 팝업으로 열도록 합니다.

> [!info] 
>  Docusaurus의 **Root.js**는 앱의 최상위 컴포넌트로, 모든 페이지에 걸쳐 공통적으로 적용되는 기능이나 스타일을 정의할 때 사용합니다. 
>  - 예: 테마 초기화, 글로벌 JavaScript 로직 실행, 글로벌 스타일 적용 등. 


## **📌 3단계: 이미지 및 동영상 확대를 위한 HTML 태그 작성 방법**
  

이제 Markdown 파일에서 이미지 및 동영상 삽입 시 **GLightbox**를 적용하는 방법입니다.

  
### **📸 이미지 예시:**

```
<a href="/static/img/example-image.png" class="glightbox">
  <img src="/static/img/example-image.png" alt="예시 이미지" />
</a>
```

- 이미지를 클릭하면 확대됩니다.


  

### **🎥 동영상(MP4) 예시:**

```
<a href="/static/videos/example-video.mp4" class="glightbox">
  <video width="100%" muted autoplay loop controls>
    <source src="/static/videos/example-video.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</a>
```

- 동영상을 클릭하면 원본 크기로 확대 재생됩니다.
    

---

## **🔄 4단계: 기존 JavaScript 기반 확대 기능 제거하기 (필수는 아니나 권장)**

  

기존에 사용했던 JavaScript 기반의 확대 기능은 GLightbox와 충돌 가능성이 있으므로, 다음 파일을 삭제하거나 Docusaurus의 docusaurus.config.js에서 기존 스크립트 로딩을 제거합니다.

- 기존 파일 예: /src/js/image-zoom.js
    

  

기존의 scripts 항목 예시:

```
scripts: [
  { src: '/js/image-zoom.js', async: true }, // 이 항목을 제거
],
```

  

---

## **🎨 5단계: 빌드 및 실행하기**

  

변경 사항을 적용한 후 빌드 및 실행하여 동작을 확인합니다.

```
npm run build
npm run serve
```

또는 개발 서버에서 바로 확인:

```
npm run start
```

  

---

## **✨ 적용 결과 및 UX 개선점**

  

이렇게 설정하면:

- 이미지 및 비디오를 클릭할 때 GLightbox가 부드럽고 현대적인 애니메이션으로 확대 팝업을 표시합니다.
    
- 모바일에서도 터치 제스처를 지원하여 사용자 경험이 크게 향상됩니다.
    
- 동영상 재생 시 확대된 화면에서 자동 재생 및 반복 재생이 가능합니다.
    

---

## **🚩 결론**

  

GLightbox를 활용한 이미지 및 비디오 확대 구현은 아래와 같은 장점이 있습니다.

- **강력한 사용자 경험(UX)** 제공
    
- **장기 유지보수성** 향상
    
- **모바일 기기 최적화** 및 호환성 보장
    

  

기존 자바스크립트 방식을 대체하여 이 방식으로 전환하시면, 향후 관리가 더욱 편리해지고 품질 높은 기술 블로그로 성장할 수 있습니다.