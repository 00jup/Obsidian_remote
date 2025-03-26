
```zsh


zsh-syntax-highlighting & zsh-autosuggestions & autojump & lsd 설치

git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  ~/.oh-my-zsh/custom/plugins/zsh-syntax-%% highlighting %%
brew install autojump
brew install lsd

~/.zshrc에 추가

# Oh my zsh
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(
  git
  zsh-syntax-highlighting
  zsh-autosuggestions
  autojump
)
source $ZSH/oh-my-zsh.sh



git aliases는 여기서 보기

lsd 설치

brew install lsd

~/.zshrc aliase

# lsd
alias ls="lsd"
alias ll="lsd -l"
alias lt="lsd --tree --depth=1"
alias lt2="lsd --tree --depth=2"
alias lt3="lsd --tree --depth=3"
alias ltl="lsd --tree"

autojump는 한 번이라도 cd 명령어로 이동한 디렉토리에 대해 사용 가능
```