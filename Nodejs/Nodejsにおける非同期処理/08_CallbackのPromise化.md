# Callback の Promise 化

Callback による非同期処理は Callback を Promise オブジェクトでラップすることで Promise 化できる

```js
const { readFile, writeFile, chmod } = require("fs");

const readFileAsync = (path) => {
  return new Promise((resolve, reject) => {
    readFile(path, (err, data) => {
      if (err) {
        reject(err);
        return;
      }
      resolve(data);
    });
  });
};

const writeFileAsync = (path, data) => {
  return new Promise((resolve, reject) => {
    writeFile(path, data, (err) => {
      if (err) {
        reject(err);
        return;
      }
      resolve();
    });
  });
};

const chmodAsync = (path, mode) => {
  return new Promise((resolve, reject) => {
    chmod(backupFile, mode, (err) => {
      if (err) {
        reject(err);
        return;
      }
      resolve();
    });
  });
};

const backupFile = `${__filename}-${Date.now()}`;

readFileAsync(__filename)
  .then((data) => {
    return writeFileAsync(backupFile, data);
  })
  .then(() => {
    return chmodAsync(backupFile, 0o400);
  })
  .catch((err) => {
    console.error(err);
  });
```
