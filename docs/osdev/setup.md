参考: https://zenn.dev/yubrot/articles/d6e85d12ccf2c6

nightlyのインストールが必要
https://doc.rust-lang.org/book/appendix-07-nightly-rust.html

下記のコマンドが必要
```
rustup component add rust-src --toolchain nightly-x86_64-unknown-linux-gnu
```

あとから変更する場合は下記のコマンドも必要
```
rustup override set nightly
```

```
error: cannot find macro `asm` in this scope
  --> /home/guy/.cargo/registry/src/index.crates.io-6f17d22bba15001f/qemu-exit-2
.0.1/src/x86.rs:24:9
   |
24 |         asm!(
   |         ^^^
   |
help: consider importing this macro
   |
7  + use core::arch::asm;
   |

error: cannot find macro `asm` in this scope
  --> /home/guy/.cargo/registry/src/index.crates.io-6f17d22bba15001f/qemu-exit-2
.0.1/src/x86.rs:55:17
   |
55 |                 asm!("hlt", options(nomem, nostack));
   |                 ^^^
   |
help: consider importing this macro
   |
7  + use core::arch::asm;
   |

error[E0463]: can't find crate for `alloc`
  --> /home/guy/.cargo/registry/src/index.crates.io-6f17d22bba15001f/uefi-0.11.0
/src/lib.rs:40:1
   |
40 | extern crate alloc as alloc_api;
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ can't find crate

error: could not compile `qemu-exit` (lib) due to 2 previous errors
warning: build failed, waiting for other jobs to finish...
For more information about this error, try `rustc --explain E0463`.
error: could not compile `uefi` (lib) due to previous error

```
とりあえずコンパイルすると上記のようなエラーがでた。
1つめの`asm`については強引にregistoryのソースを修正したところOK
 → ちゃんとした解決方法があれば知りたい
2つめの`alloc`については`config.toml`に下記を追記することで回避した。
```
- build-std = ["core", "compiler_builtins", ]
+ build-std = ["core", "compiler_builtins", "alloc"]
```

RustのWorkspaceの作りかたはこれ
https://doc.rust-jp.rs/book-ja/ch14-03-cargo-workspaces.html

<ブートローダービルド問題>
edk2-stable202102

```
build.py...
 : error 7000: Failed to execute command
        make tbuild [/home/guy/edk2/Build/EmulatorX64/DEBUG_CLANG38/X64/EmulatorPkg/Unix/Host/Host]
/home/guy/edk2/BaseTools/BinWrappers/PosixLike/../../Source/Python/build/build.py:500: DeprecationWarning: isSet() is deprecated, use is_set() instead
  if BuildTask._ErrorFlag.isSet():
/home/guy/edk2/BaseTools/BinWrappers/PosixLike/../../Source/Python/build/build.py:505: DeprecationWarning: getName() is deprecated, get the name attribute instead
  EdkLogger.debug(EdkLogger.DEBUG_8, "Threads [%s]" % ", ".join(Th.getName() for Th in threading.enumerate()))


build.py...
 : error F002: Failed to build module
        /home/guy/edk2/EmulatorPkg/Unix/Host/Host.inf [X64, CLANG38, DEBUG]

- Failed -
Build end time: 10:02:06, Jul.28 2023
Build total time: 00:00:29
```
edk2-stable202208
↑と同じエラー
https://github.com/uchan-nos/os-from-zero/issues/97
を試してみたが、できず。

以下の対応忘れていた。。やっとビルドができた
 - ACTIVE_PLATFORM       = EmulatorPkg/EmulatorPkg.dsc
 + ACTIVE_PLATFORM       = MikanLoaderPkg/MikanLoaderPkg.dsc

 - TARGET_ARCH           = IA32
 + TARGET_ARCH           = X64

 - TOOL_CHAIN_TAG        = VS2015x86
 + TOOL_CHAIN_TAG        = CLANG38


<カーネルのピクセル描画がされない問題>
ld.lldに-z separate-code を追加


