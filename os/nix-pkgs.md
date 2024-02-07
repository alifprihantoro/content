# install and setup
## install pkgs
### from nix os
### from nix pkgs
```bash
# install
nix-env -iA <name-channels>.<name-pkgs>
# list pkgs installed 
nix-env -q --installed
# rm packages
nix-env -e <name-pkgs>
# update
nix-channel --update
nix-env -u
# remove
nix-collect-garbage
# swich version
nix-shell -p <name-with-ver>
```
### home manager
```bash
nix-channel --add https://github.com/nix-community/home-manager/archive/master.tar.gz home-manager
nix-channel --add https://nixos.org/channels/nixpkgs-unstable nixpkgs
nix-channel --update
nix-shell '<home-manager>' -A install

```
### direnv
```bash
# direnv must be installed
echo "use flake" > .envrc
eval "$(direnv hook zsh)"
direnv
nix build
```
configs :
```nix
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs";
    utils.url =  "github:numtide/flake-utils";
  };

  outputs = {self, ...}@inputs:
    inputs.utils.lib.eachDefaultSystem (system:
    let
      inherit (lib) attrValues;
      pkgs = inputs.nixpkgs.legacyPackages.${system};
      lib = inputs.nixpkgs.lib;
    in
      rec {
        devShell = with pkgs; mkShell {
          buildInputs = [
            nodejs_20
            nodePackages.pnpm
          ];
        };
      }
    );
}
```
