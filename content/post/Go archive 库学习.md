{
    "date": "2015-08-03",
    "description": null,
    "draft": false,
    "id": 16,
    "image": null,
    "meta_title": null,
    "slug": "Go-stdandard-lib-archive",
    "tags": [
        "Go",
        "lib",
        "archive"
    ],
    "title": "Go archive 标准库学习",
    "type": "post"
}

archive 包含 tar 和 zip

tar 包实现了对 tar 压缩格式的访问，旨在覆盖包括 GNU 和 BSD tar 在内的大多数变体。

官方例子，增加把压缩文件写出

```go
package main

import (
    "archive/tar"
    "bytes"
    "fmt"
    "io"
    "io/ioutil"
    "log"
    "os"
)

func main() {
    // Create a buffer to write our archive to.
    buf := new(bytes.Buffer)

    // Create a new tar archive.
    tw := tar.NewWriter(buf)

    // Add some files to the archive.
    var files = []struct {
        Name, Body string
    }{
        {"readme.txt", "This archive contains some text files."},
        {"gopher.txt", "Gopher names:\nGeorge\nGeoffrey\nGonzo"},
        {"todo.txt", "Get animal handling licence."},
    }
    for _, file := range files {
        hdr := &tar.Header{
            Name: file.Name,
            Size: int64(len(file.Body)),
        }
        if err := tw.WriteHeader(hdr); err != nil {
            log.Fatalln(err)
        }
        if _, err := tw.Write([]byte(file.Body)); err != nil {
            log.Fatalln(err)
        }
    }
    // Make sure to check the error on Close.
    if err := tw.Close(); err != nil {
        log.Fatalln(err)
    }

    // Write to file
    if err := ioutil.WriteFile("archive.tar", buf.Bytes(), 0644); err != nil {
        log.Fatalln(err)
    }

    // Open the tar archive for reading.
    r := bytes.NewReader(buf.Bytes())
    tr := tar.NewReader(r)

    // Iterate through the files in the archive.
    for {
        hdr, err := tr.Next()
        if err == io.EOF {
            // end of tar archive
            break
        }
        if err != nil {
            log.Fatalln(err)
        }
        fmt.Printf("Contents of %s:\n", hdr.Name)
        if _, err := io.Copy(os.Stdout, tr); err != nil {
            log.Fatalln(err)
        }
        fmt.Println()
    }
}
```
文件介绍

tar

- common.go 提供常量和通用函数的定义
- reader.go 提供对 tar 文件的访问
- writer.go 提供对 tar 文件的写


zip 提供对 zip 格式的文件的读写操作

```go
// Copyright 2012 The Go Authors. All rights reserved.
// Use of this source code is governed by a BSD-style
// license that can be found in the LICENSE file.

package main

import (
    "archive/zip"
    "bytes"
    "fmt"
    "io"
    "io/ioutil"
    "log"
    "os"
)

func ExampleWriter() {
    // Create a buffer to write our archive to.
    buf := new(bytes.Buffer)

    // Create a new zip archive.
    w := zip.NewWriter(buf)

    // Add some files to the archive.
    var files = []struct {
        Name, Body string
    }{
        {"readme.txt", "This archive contains some text files."},
        {"gopher.txt", "Gopher names:\nGeorge\nGeoffrey\nGonzo"},
        {"todo.txt", "Get animal handling licence.\nWrite more examples."},
    }
    for _, file := range files {
        f, err := w.Create(file.Name)
        if err != nil {
            log.Fatal(err)
        }
        _, err = f.Write([]byte(file.Body))
        if err != nil {
            log.Fatal(err)
        }
    }

    // Make sure to check the error on Close.
    err := w.Close()
    if err != nil {
        log.Fatal(err)
    }

    // Write to file
    if err := ioutil.WriteFile("1.zip", buf.Bytes(), 0644); err != nil {
        log.Fatalln(err)
    }
}

func ExampleReader() {
    // Open a zip archive for reading.
    r, err := zip.OpenReader("testdata/readme.zip")
    if err != nil {
        log.Fatal(err)
    }
    defer r.Close()

    // Iterate through the files in the archive,
    // printing some of their contents.
    for _, f := range r.File {
        fmt.Printf("Contents of %s:\n", f.Name)
        rc, err := f.Open()
        if err != nil {
            log.Fatal(err)
        }
        _, err = io.CopyN(os.Stdout, rc, 68)
        if err != nil {
            log.Fatal(err)
        }
        rc.Close()
        fmt.Println()
    }
    // Output:
    // Contents of README:
    // This is the source code repository for the Go programming language.
}

func main() {
    ExampleReader()
    ExampleWriter()
}
```


