# Maintainer: Vitaly Ankh (vitalyr) <vitalyankh@gmail.com>
# Contributor: Ignacy Kuchciński (ignapk) <ignacykuchcinski@gmail.com>
# Contributor: Simon Gardling <titaniumtown@gmail.com>
# Contributor: Ricardo Liang (rliang) <ricardoliang@gmail.com>

pkgname=mutter-git
_pkgname=mutter
pkgver=42.rc+2+g73780ea76
pkgrel=1
pkgdesc="A window manager for GNOME."
url="https://gitlab.gnome.org/GNOME/mutter"
arch=(x86_64)
license=(GPL)
depends=(dconf gobject-introspection-runtime gsettings-desktop-schemas
         libcanberra startup-notification zenity libsm gnome-desktop upower
         libxkbcommon-x11 gnome-settings-daemon libgudev libinput pipewire
         xorg-xwayland graphene libxkbfile)
makedepends=(gobject-introspection git egl-wayland meson xorg-server
             wayland-protocols)
provides=(mutter)
conflicts=(mutter)
groups=(gnome)
source=("git+https://gitlab.gnome.org/GNOME/mutter.git")
sha256sums=('SKIP' 'SKIP')

prepare() {
  cd $_pkgname
}

pkgver() {
  cd $_pkgname
  git describe --tags | sed 's/-/+/g'
}

build() {
  arch-meson $_pkgname build \
    -D egl_device=true \
    -D wayland_eglstream=true \
    -D installed_tests=false \
    -D profiler=false
  meson compile -C build
}

package() {
  DESTDIR="$pkgdir" meson install -C build
}
