# Function_Collection

## Go
<details>
  <summary>getPaths(获取文件或者目录下的所有文件)</summary>
  
  ```go
  func getPaths(fnames []string) (paths []string, haveFolder bool, err error) {
    haveFolder = false
    paths = []string{}
    for _, fname := range fnames {
      stat, errStat := os.Stat(fname)
      if errStat != nil {
        err = errStat
        return
      }
      if stat.IsDir() {
        haveFolder = true
        err = filepath.Walk(fname,
          func(pathName string, info os.FileInfo, err error) error {
            if err != nil {
              return err
            }
            if !info.IsDir() {
              paths = append(paths, filepath.ToSlash(pathName))
            }
            return nil
          })
        if err != nil {
          return
        }
      } else {
        paths = append(paths, filepath.ToSlash(fname))
      }
    }
    return
  }
  ```
</details>  
