# Compiling

## Fedora based Linux

First install the required dependencies:

```
sudo dnf groupinstall "Development Tools"
sudo dnf install gnu-efi
```

Now install the kernel dev packages

```
sudo dnf install kernel-devel kernel-headers
```

Finish it with the following:

```
sudo make
```

## Debian based Linux

First install the required dependencies:

```
sudo apt install build-essentials gnu-efi
```

Now install the kernel dev packages

```
sudo apt install kernel-dev linux-headers
```

Finish it with the following:

```
sudo make
```
