# Jellyfin Setup
## Data Directory
### Folder Mapping
It's good practise to give all containers the same access to the same root directory or share. This is why all containers in the compose file have the bind volume mount ```/data:/data```. It makes everything easier, plus passing in two volumes such as the commonly suggested /tv, /movies, and /downloads makes them look like two different file systems, even if they are a single file system outside the container. See my current setup below.

> [!NOTE]
> For simplicity and compatibility it is recommended to install Jellyfin with Docker in a __virutal machine__ if you're running Proxmox. See more information [here](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#chapter_pct).
>

```
data
├── movies
├── music
└── shows
docker
└── jellyfin
    └── config
```

### Docker Setup
Docker is another option to install and run Jellyfin. Checkout the compose.yaml for the full stack.

#### Hardware Transcoding
This focuses on trascoding with Intel QuickSync. In my experiance it is simply the best option. If you're running a AMD CPU you can pickup a Intel Arc GPU fairly cheap. If you have any issues or don't have access to a Intel CPU or an Arc GPU be sure to checkout the offical docs [here](https://jellyfin.org/docs/general/administration/hardware-acceleration/). If you're not doing this on Proxmox you can skip to the Ubuntu setup.

### Proxmox Passthough

> [!NOTE]
> Running Jellyfin with Docker on a VM is highly recommened. This elimates permissions issues with running Jellyfin on the system and running Docker on a VM is what is recommended by the Proxmox team.
>

#### Running on a VM (Recommened)
Under your virutal machine Proxmox click the Hardware option on the sidebar. From there select Add > PCI Device. Then select Raw and pick the device that we will use for Quicksync or another GPU if you're not using Quicksync. For Quicksync it's often the very first Intel device that will say something like "Alderlake" in the name.

### Ubuntu Setup
The following steps take place on the Ubuntu server virtual machine. Add jellyfin (and the user you're running jellyfin as that) to the render group.
```
sudo usermod -aG render jellyfin
sudo usermod -aG render julian # since I'm running jellyfin as my user
sudo systemctl restart jellyfin
```
Now we can confirm hardware transcoding is ready by intstalling the `intel-gpu-tools` package and running the command `intel_gpu_top`.
```
sudo apt install intel-gpu-tools
intel_gpu_top
```

## Configuring Jellyfin
Open your web browser and navigate to your installed instance of Jellyfin using `http://IP:8096` and once there you can power through the initial setup by selecting your preferred language, then create an admin account with a secure username and password. Next, set up your media libraries by adding folders for movies, TV shows, or music. I tend to keep everything in my `/data` directory as shown in the media page on this repo.

## Plugins
Below are the plugins I'm currently testing. I'd recommend checking out [Awesome Jellyfin](https://github.com/awesome-jellyfin/awesome-jellyfin) for much more.

1. [Intro Skipper](https://github.com/intro-skipper/intro-skipper)
