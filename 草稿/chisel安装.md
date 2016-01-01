# Chisel安装

brew update
brew install chisel
Then follow the instructions that Homebrew displays to add chisel to your ~/.lldbinit.

Add the following line to ~/.lldbinit to load chisel when Xcode launches:
  command script import /usr/local/opt/chisel/libexec/fblldb.py