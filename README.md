# JavaScript-Count-the-longest-path
daily coding challenge #17

```
function longestFilePath(fileSystem) {
  // \n and \t are considered one character

  // key: level, value: the longest folder length at this level
  // By default, we start level 0 with length of 0, and dir to be level 1
  // and dir under dir is at level 2
  const levels = new Map();
  levels.set(0, 0);
  let longest = 0;
  const files = fileSystem.split('\n'); // folders are considered files

  // Could have used an array of length files + 1 instead of a map

  for (let i = 0; i < files.length; i++) {
    const file = files[i];
    // if there is no last index of, it returns -1 and we add 1 to turn to 0
    const level = file.lastIndexOf('\t') + 1; // the amount of \t determines its level
    const fileLength = file.length - level;

    if (file.includes('.')) {
      // actual file
      longest = Math.max(longest, levels.get(level) + fileLength);
    } else {
      const lastLevel = levels.get(level);
      levels.set(level + 1, lastLevel + fileLength + 1); // plus 1 includes the '/' for each level
      // do not have the find the max length for each level because the file system goes down level by level
      // Once we're done with one folder, we go to the second folder and update it's length at that level
    }
  }
  return longest;
}

longestFilePath("dir\n\tsubdir1\n\tsubdir2\n\t\tfile.ext"), 20]
```
