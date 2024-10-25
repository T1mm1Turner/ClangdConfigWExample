# Query Driver Config for [Clangd](https://clangd.llvm.org/) with [coc-clangd](https://github.com/clangd/coc-clangd) on windows.

## Since docs of clangd are ambiguous here is my explain.

Clangd server works by default with unix like systems, so, if you try to use standard library with vim (for example) it'll be annoying to put the include paths manual.

The solution for this is: the [--query-driver](https://clangd.llvm.org/guides/system-headers#query-driver). Clangd comes with a command line option that ask the passed compiler for library database, but, this is an exclusive option of clangd and this is depending on the way you call clangd, in my case with [coc](https://github.com/neoclide/coc.nvim) with :CocConfig in vim (notice the absolute path):

```json
{
    "clang.path": "~\\.config\\coc\\extensions\\coc-clangd-data\\\\install\\18.1.3\\clangd_18.1.3\\bin\\clangd.exe",
    "clang.arguments: ["--query-driver=C:\\msys64\\ucrt64\\bin\\gcc.exe"]
}
```

Since im using gcc for the library database its necesary to use the compiler to, and this is made with the [clangd compiler](https://clangd.llvm.org/config#compiler) (inside the config.yaml and with the absolute path):

```yaml
CompileFlags:
# If we made it manually.
# Add: [-isystemC:\msys64\ucrt64\include\c++\14.1.0, -isystem-afterC:\msys64\ucrt64\lib\gcc\x86_64-w64-mingw32\14.1.0]
    # So much easy.
    Compiler: C:\msys64\ucrt64\bin\gcc.exe
```