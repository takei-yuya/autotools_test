複数のディレクトリから同じディレクトリのソースファイルを参照していて、
かつ、 `AM_INIT_AUTOMAKE` のオプションに `subdir-objects` を指定した時に、
`make distclean` したときに `src/.deps/a.Po: No such file or directory` とか言われるやーつ


挙動としては、SUBDIR側の `Makefile` の `distclean` が、`.deps/` ごと消してしまって、
`.` の `Makefile` が、依存解析のために `.deps/***.Po` を `include` しているので死ぬやつ。

Automake 1.16.1 では、 `.deps/` は消さず、 `.deps/***.Po` だけ消すので、ファイルが異なれば問題が起きない
のと、 include するファイルが無くても致命的なエラーにならない様子？
