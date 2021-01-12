# m1_mac_config
My 2 cents for setting up M1 Mac developing env natively.

### Shell
- Default terminal comes with zsh, just need to install oh-my-zsh as usual.
- Configure the plugins (zsh-autosuggestions zsh-syntax-highlighting, etc.)


### Xcode
- Install Xcode. For the first time only, open xcode from Applications, agree to the terms.
- Install command line tools using "xcode-select --install".


### Homebrew
- As of now, homebrew can be installed natively, though some formulas might not work.
- /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"


### Python
##### Miniforge
- Install mini forge from https://github.com/conda-forge/miniforge (select architecture arm64).
##### Jupyter
- Follow the issue here: https://github.com/jupyter/notebook/issues/5882
- As of now, “conda install jupyter” would result in unexplained conflict, use “conda install jupyterlab” instead.
- Modify _use_appnope function of “miniforge3/envs/YOURENV/lib/python3.X/site-packages/ipykernel/eventloops.py”
```
def _use_appnope():
  """Should we use appnope for dealing with OS X app nap?
  Checks if we are on OS X 10.9 or greater.
  """
  return sys.platform == 'darwin' and V(platform.mac_ver()[0]) >= V('10.9') and platform.mac_ver()[2] != 'arm64'
```
- Use “conda install jedi==0.17.2” if your kernel would die when autocompleting (a bug of jedi 0.18.0?)
##### OpenAI Gym
- Follow the rendering issue here: https://github.com/pyglet/pyglet/pull/335
- As of now, “pip install --user --upgrade git+http://github.com/pyglet/pyglet@pyglet-1.5-maintenance”
##### PyTorch
- Follow the issue here: https://github.com/pytorch/pytorch/issues/48145
- In the above link, people have built wheel for python 3.8 and 3.9 which you can use (CPU only, OpenMP disabled).


### Vim
- Install vim-plug as usual.
- Create .vimrc as you like it (a sample one is attached).
- Install node via nvm (node version manager) if you would like to use neoclide/coc.nvim plug (coc-nvim).
- curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
- nvm install v15
- If using coc-nvim, open up a .py file and install coc python “CocInstall coc-python”.


### VS code
- Download insider version https://code.visualstudio.com


### IDEs
- IntelliJ for Apple Silicon is available.


### OpenMP
- Default clang does not support OpenMP. The easiest solution is to "brew install libomp" and take care of some extra compilation flags.
- Info in this link is still valid https://iscinumpy.gitlab.io/post/omp-on-high-sierra/


### Accelerate
- “-framework Accelerate” compilation flag still works if your project needs LAPACK, BLAS.
