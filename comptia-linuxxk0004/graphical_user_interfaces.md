Filename: comptia-linuxxk0004-8-1-1-graphical_user_interfaces  
Show Name: CompTIA Linux+ (XK0-004)  
Topic: Managing System Components  
Episode Name: Graphical User Interfaces  
Description: In this episode, Zach and Don introduce the viewers to some of the graphical user interfaces found in Linux. They explain how the X Windows subsystem powers most GUIs and then tour the GNOME and KDE desktop environments.

---

### Graphical User Interfaces

#### What are some of the things a GUI can help us with?

---

- Benefits
  - Provides easy access
  - Complex concepts represented as images
- Not always needed
  - Consumes resources
  - Not usually present on a server

#### What powers the GUI behind the scenes?

---

- Components
  - X Client
    - AKA Desktop Environment
    - AKA Window Manager
  - X Server
  - Compositor
  - I/O Hardware
- Can deliver graphics remote
  - Xrdp
  - VNC
  - SSH Tunneling

#### So X is pretty important. Did Linus Torvalds create it as well?

---

- Developed at MIT in 1984
  - X11
  - [XFree86 Website](https://www.xfree86.org/)
- Forked to X.org in 2004 due to licensing
  - [X.Org Website](https://www.x.org/)

#### Does every distribution use the X.Org Server?

---

- Wayland
  - [Wayland Website](https://wayland.freedesktop.org/)
  - Released in 2008
  - Combines X Server and Compositor
  - Default in Fedora
  - Not perfect yet

#### Let's switch to the client side. What are the predominant X Clients out there?

---

- [GNOME](https://www.gnome.org/)
  - Simple design
  - Excellent accessibility
    - `Settings -> Universal Access`
- [MATE Desktop](https://mate-desktop.org/)
  - Forked from GNOME v2

#### Who comes in second place for GUIs?

---

- [KDE Plasma](https://kde.org/plasma-desktop)
  - Modular widgets
  - Vast customization
  - Large suite of native apps

#### Can we run KDE and GNOME on the same system?

---

- `yum groupinstall "KDE Plasma Workspaces"`
