# 📄 Obsidian Image Link Converter

This script converts image links like:

    `![[image.png]]`

to:

    `![](/images/image.png)`

for use in Docusaurus.

## **✅ 주요 기능**

| **기능**         | **설명**                                         |
| -------------- | ---------------------------------------------- |
| Obsidian 링크 변환 | `![[image.png]] → ![](/images/image.png)`      |
| 사이즈 포함 처리      | `![[image.png\|200]] → ![](/images/image.png)` |
| 이미지 존재 확인      | /static/images/image.png 없으면 ⚠️ 경고 출력          |
| 원본 백업          | _backup/ 폴더에 자동 저장                             |

  
## 🛠 Python 코드 예시


```python
import os
import re
import shutil

def convert_obsidian_links(text, missing_images, image_dir):
    def replacer(match):
        filename = f"{match.group(1)}.{match.group(2)}"
        if not os.path.exists(os.path.join(image_dir, filename)):
            missing_images.add(filename)
        return f"![](/images/{filename})"

    # Convert Obsidian-style links with or without sizing
    return re.sub(r'!\[\[([\w\-.]+)\.(png|jpg|jpeg|gif|svg)(\|\d+)?\]\]', replacer, text)

def process_markdown_files(folder, static_image_path, backup=True):
    backup_dir = os.path.join(folder, "_backup")
    if backup and not os.path.exists(backup_dir):
        os.makedirs(backup_dir)

    missing_images = set()

    for root, _, files in os.walk(folder):
        for file in files:
            if file.endswith(".md"):
                filepath = os.path.join(root, file)
                rel_path = os.path.relpath(filepath, folder)
                backup_path = os.path.join(backup_dir, rel_path)

                # Make backup
                if backup:
                    os.makedirs(os.path.dirname(backup_path), exist_ok=True)
                    shutil.copy2(filepath, backup_path)

                # Read and convert
                with open(filepath, "r", encoding="utf-8") as f:
                    content = f.read()
                updated = convert_obsidian_links(content, missing_images, static_image_path)

                # Write back
                with open(filepath, "w", encoding="utf-8") as f:
                    f.write(updated)
                print(f"✔ Converted: {filepath}")

    if missing_images:
        print("\n⚠️  아래 이미지 파일이 static/images 폴더에 존재하지 않습니다:")
        for img in sorted(missing_images):
            print(f" - {img}")
    else:
        print("\n✅ 모든 참조 이미지가 존재합니다.")

if __name__ == "__main__":
    target_folder = input("🔍 변환할 폴더 경로를 입력하세요 (예: ./vault): ").strip()
    image_folder = input("🖼  이미지 폴더 경로를 입력하세요 (예: ./static/images): ").strip()

    if os.path.isdir(target_folder) and os.path.isdir(image_folder):
        process_markdown_files(target_folder, image_folder)
        print("\n✅ 변환이 완료되었습니다. 기존 파일은 '_backup/' 폴더에 백업되었습니다.")
    else:
        print("❌ 유효한 폴더 경로를 입력하세요.")
- `.md` 파일 전체를 변환하고, 이미지 링크를 깨지지 않게 유지합니다.      
```


  

👉 [convert_obsidian_images_with_check.py 다운로드](sandbox:/mnt/data/convert_obsidian_images_with_check.py?_chatgptios_conversationID=6809f5ee-b154-8008-a5bf-ad39112118e6&_chatgptios_messageID=6f26984a-d728-4f32-a200-0583e90173d9)

![[template/convert_obsidian_images_with_check.py]]


## **🧠 사용법**

```
python convert_obsidian_images_with_check.py
```

### **입력:**

```
🔍 변환할 폴더 경로를 입력하세요 (예: ./vault)
🖼  이미지 폴더 경로를 입력하세요 (예: ./static/images)
```

변환 후, 누락된 이미지 목록을 아래처럼 출력:

```
⚠️  아래 이미지 파일이 static/images 폴더에 존재하지 않습니다:
 - diagram.png
 - setup-guide.jpg
```

  
