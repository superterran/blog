---

date: 2021-05-01

---





It's like a water-shed moment over at the GNOME extensions site as a few blurring modules are finally starting to surface. r/unixporn is on fire with screenshots. So let's so do a little something for the kids. Let's blur our shells...

Of all the themes I've seen come through so far, this one seems like the most interesting. 

[materia-theme-transparent/INSTALL.md at master · ckissane/materia-theme-transparent · GitHub](https://github.com/ckissane/materia-theme-transparent/blob/master/INSTALL.md)

The installation instructions are basically as follows:

```bash
sudo dnf install meson
mkdir -p ~/bin
cd ~/bin
git clone git@github.com:ckissane/materia-theme-transparent.git
cd materia-theme-transparent
meson _build
meson install -C _build
```

Once done, no need to logout or anything, fire up the Tweaks app, go to Appearance, and select one of the variants you just installed and vola!

![https://i.imgur.com/xmhlizn.jpg](https://i.imgur.com/xmhlizn.jpg)

GNOME is starting to look pretty spectacular! Now let's just see how stable it is.
