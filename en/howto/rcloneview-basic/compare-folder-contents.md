---
sidebar_position: 3
description: This is sample Post for writer
keywords:
  - rcloneview
  - howto
  - cloud
  - sync
  - rclone
tags:
  - RcloneView
  - howto
  - Cloud
  - Sync
date: 2025-05-30
author: Jay
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Compare folder contents

RcloneView helps you identify differences between two folders—whether on local disk or across cloud remotes—and copy or manage files efficiently using its built-in Compare feature.

## Selecting Folders to Compare

To begin comparing folders:
- Open two tabs in the Explorer pane.
- Select the folders you want to compare from the folder tree or manually enter the full path using the Path Bar.
- Click the **`Compare`** button in the top **`Home`** menu to start the comparison.

<img src="/support/images/en/howto/rcloneview-basic/select-compare-folder.png" alt="select compare folder" class="img-medium img-center" />
When the comparison is complete, a summary popup will appear.
To disable this message in the future, check **“Don’t show this message again.”**
<img src="/support/images/en/howto/rcloneview-basic/folder-comparison-completed.png" alt="folder comparison completed" class="img-medium img-center" />
For details about the layout of the folder comparison screen and the meaning of each icon, please refer to the guide of folder comparision.

## Compare Results and Manage Files

Folder comparison allows you to directly compare and select files for management.

However, if you need to sync large folders or manage multiple remote folders efficiently, using the **`Sync`** is a more convenient method.

### Display by selected result type

You can filter the comparison results to display only the files relevant to your operation.  
This helps you focus on what needs to be copied or reviewed.

For example, if you want to copy files from the left remote's folder to the right's:

- Click the **`Show left-only files`** icon <img src="/support/icons/show-left-only-files.png" alt="show left only files" class="inline-icon" /> to display only files that exist in the left folder but not in the right.
- Click the **`Show different files`** icon <img src="/support/icons/show-different-files.png" alt="show different files" class="inline-icon" /> to display files that exist in both folders but differ in size.
- This way, you can focus only on the target files for copying to the right side, without being distracted by already synced files.

> ✅ This makes it much easier to select and copy only the necessary files in one direction.
<img src="/support/images/en/howto/rcloneview-basic/compare-display-select.png" alt="compare display select" class="img-medium img-center" />



<details>
<summary>More Icon details</summary>

<Tabs>
<TabItem value="Display Icons" label="Display Icons">
When you click each icon with the mouse, the following filtering behavior is applied.  
Clicking again will toggle the filter on or off.

When multiple icons are selected, files matching **any** of the selected conditions are displayed (logical **OR**).

<img src="/support/icons/show-left-only-files.png" alt="show left only files" class="inline-icon" /> : Display only files that exist in the left folder but not in the right.

<img src="/support/icons/show-left-only-files.png" alt="show left only files" class="inline-icon" /> : Display only files that exist in the right folder but not in the left.

<img src="/support/icons/same-file-icon.png" alt="same file icon" class="inline-icon" /> : Display only files that exist in both folders and are identical.

<img src="/support/icons/show-different-files.png" alt="show different files" class="inline-icon" />  : Display files that exist in both folders but differ in size.

<img src="/support/icons/show-errored-files.png" alt="show errored files" class="inline-icon" /> : Display any errors or confilcts

</TabItem>

<TabItem value="Navigate Icons" label="Navigate Icons">
These icons are used in the **Compare** view to move up or down through the folder hierarchy based on the current flat folder list structure.

<img src="/support/icons/navigate-to-upper-folder.png" alt="navigate to upper folder" class="inline-icon" /> : Navigate to the **Upper folder** in the current list.

<img src="/support/icons/navigate-to-lower-folder.png" alt="navigate to lower folder" class="inline-icon" /> : Navigate to the **Lower folder** in the current list.

</TabItem>

<TabItem value="Operation Icons" label="Operation Icons">
These icons are used to perform file operations within folders—such as deleting files or copying them to the left or right.

<img src="/support/icons/copy-file-to-right.png" alt="copy file to right" class="inline-icon" /> : Copy selected files to the right folder.

<img src="/support/icons/copy-files-to-left.png" alt="copy files to left" class="inline-icon" /> : Copy selected files to the left folder.

<img src="/support/icons/delete-files.png" alt="delete files" class="inline-icon" /> : Delete selected files from either side.

</TabItem>

<TabItem value="Find Icons" label="Find Icons">
The **Find** icons are used in the **Compare view** to locate folders where file count or file size changes are most significant.

<img src="/support/icons/find-folder-by-count.png" alt="find folder by count" class="inline-icon" /> : Find folders based on the number of files changed during comparison.

<img src="/support/icons/find-folder-by-size.png" alt="find folder by size" class="inline-icon" /> : Find folders based on the total size of files changed during comparison.

<img src="/support/icons/find-folder-with-largest-change.png" alt="find folder with largest change" class="inline-icon" /> : Find and move to the folder with the most significant file count or size change.

<img src="/support/icons/find-folder-with-next-large-change.png" alt="find folder with next large change" class="inline-icon" /> : Move to the next folder with a larger file count or size difference.

<img src="/support/icons/find-folder-with-smallest-change.png" alt="find folder with smallest change" class="inline-icon" /> : Find and move to the folder with the least amount of change.

<img src="/support/icons/find-folder-with-next-smaller-change.png" alt="find folder with next smaller change" class="inline-icon" /> : Move to the next folder with a smaller file count or size change.

</TabItem>

</Tabs>


</details>


### Copying files between remote folders

#### Select files to copy

- Use `Ctrl + Click` to select individual files
- Use `Shift + Click` to select a range
- Or simply use drag and drop between panels

#### Perform copy operation

Once files are selected:
- Click the **`Copy →`** button to copy the selected files from the left side to the right side.
- Click the **`← Copy`** button to copy from right to left.

💡 Copy only occurs if:
- The file doesn't exist on the target side
- The file exists in both sides but has a different size

After the copy is complete:
- Copied files will be marked as **`equal`** icon <img src="/support/icons/equal-icon.png" alt="equal icon" class="inline-icon" />in the comparison view
- The status bar at the bottom will update with completion details
<div class="img-grid-2">
<img src="/support/images/en/howto/rcloneview-basic/compare-copy-operation.png" alt="compare copy operation" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/compare-copy-operation-completed.png" alt="compare copy operation completed" class="img-medium img-center" />
</div>
:::important Checksum (coming soon)
By default, RcloneView compares files by name and size.  
However, this might not be enough to detect content differences when file names and sizes are the same.
✅ Checksum comparison will allow byte-level verification of file contents.  
This feature is planned for a future update and will help ensure even greater sync accuracy.
:::
#### Deleting files

You can also delete selected files from either folder:
- Click the **`Delete`** button on the left to remove files from the left folder
- Click the **`Delete`** button on the right to remove files from the right folder

⚠️ Deletion is permanent. Double-check selected files before proceeding.
 
## Using filters to refine comparison

The filter feature allows you to run folder comparisons more efficiently by excluding specific files or folders from the result.

 :::important Plus License Required
Filtering is available in the **Plus** License version of RcloneView.
:::

### Why use filters?

You may want to exclude certain folders or file types that are not relevant to your comparison task.  
With the filter tool, you can easily define which files or folders should be ignored during comparison.

### How to exclude a specific folder:

For example, to exclude all folders named `folder2` from the comparison:
1. Click the **`Filter`** icon <img src="/support/icons/filter-run-icon.png" alt="filter run icon" class="inline-icon" /> in the Compare screen.
2. In the filter input field, type `folder2/` and click **`Add`**.
3. The folder will appear in the **`Others`** category.
4. Check the box next to `folder2/` and click **`OK`** to apply the filter.
5. Re-run the comparison.

<div class="img-grid-2">
<img src="/support/images/en/howto/rcloneview-basic/add-custom-filter-rule.png" alt="add custom filter rule" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/addjust-custom-filter-rule.png" alt="addjust custom filter rule" class="img-medium img-center" />
</div>

💡 Filtering is especially helpful when folders like `cache`, `temp`, or personal configuration directories only exist for reference and do not need to be compared or copied.



<details>
<summary>Frequently Used Filter Rules</summary>

**`.iso`** : Exclude all .iso files

**`/.git/*`** : Exclude only files inside the .git folder in the root, not subfolders

**`/.git/`** :  Exclude the entire .git folder in the root, including everything inside it

**`.git/`** :Exclude all .git folders and everything inside them, regardless of location

</details>





