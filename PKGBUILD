# Maintainer: Filip Brcic <brcha@gna.org>

_basename=octopi
pkgname=${_basename}-frameworks
pkgver=0.7.0
pkgrel=1
pkgdesc="A powerful Pacman frontend using Qt libs (Qt5 & KF5 build)"
arch=('i686' 'x86_64')
url="https://github.com/aarnt/octopi"
license=('GPL2')
install=$pkgname.install
makedepends=('automoc4' 'cmake' 'git')
depends=('qt5-base' 'qt5-declarative' 'knotifications')
provides=('octopi' 'octopi-notifier' 'octopi-repoeditor' 'octopi-cachecleaner')
conflicts=('octopi' 'octopi-notifier' 'octopi-repoeditor' 'octopi-cachecleaner' 'oktopi-git')
source=("https://github.com/aarnt/octopi/archive/v${pkgver}.tar.gz"
        'octopi-repoeditor.desktop')
sha256sums=('03d15458ebe482e5a9a00e7a3db5676a53886c754b13a7c56e36d75b73f2d496'
            '131f16745df685430db55e54ede6da66aed9b02ca00d6d873a002b2a3e1c90ef')

build() {
  msg "Building octopi..."
  cd ${srcdir}/${_basename}-${pkgver}
  qmake-qt5 octopi.pro 
  make

  msg "Building pacmanhelper..."
  cd ${srcdir}/${_basename}-${pkgver}/notifier/pacmanhelper
  qmake-qt5 pacmanhelper.pro
  make
  
  msg "Building octopi-notifier..."
  cd ${srcdir}/${_basename}-${pkgver}/notifier/octopi-notifier
  qmake-qt5 octopi-notifier.pro 'DEFINES+=KSTATUS'
  make
    
  msg "Building octopi-repoeditor..."
  cd ${srcdir}/${_basename}-${pkgver}/repoeditor
  qmake-qt5 octopi-repoeditor.pro
  make

  msg "Building octopi-cachecleaner..."
  cd ${srcdir}/${_basename}-${pkgver}/cachecleaner
  qmake-qt5 octopi-cachecleaner.pro
  make
}

package() {
  # Octopi
  cd "${srcdir}/${_basename}-${pkgver}"

  install -D -m755 "${srcdir}/${_basename}-${pkgver}/bin/octopi" "${pkgdir}/usr/bin/octopi"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/octopi.desktop" "${pkgdir}/usr/share/applications/octopi.desktop"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/resources/images/octopi_green.png" "${pkgdir}/usr/share/icons/octopi.png"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/resources/images/octopi_green.png" "${pkgdir}/usr/share/icons/gnome/32x32/apps/octopi.png"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/resources/images/octopi_red.png" "${pkgdir}/usr/share/icons/octopi_red.png"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/resources/images/octopi_yellow.png" "${pkgdir}/usr/share/icons/octopi_yellow.png"

  #Pacmanhelper service files
  install -D -m755 "${srcdir}/${_basename}-${pkgver}/notifier/bin/pacmanhelper" "${pkgdir}/usr/lib/octopi/pacmanhelper"

  install -D -m644 "${srcdir}/${_basename}-${pkgver}/notifier/pacmanhelper/polkit/org.octopi.pacman.policy" "${pkgdir}/usr/share/polkit-1/actions/org.octopi.pacman.policy"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/notifier/pacmanhelper/polkit/org.octopi.pacmanhelper.conf" "${pkgdir}/etc/dbus-1/system.d/org.octopi.pacmanhelper.conf"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/notifier/pacmanhelper/polkit/org.octopi.pacmanhelper.xml" "${pkgdir}/usr/share/dbus-1/interfaces/org.octopi.pacmanhelper.xml"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/notifier/pacmanhelper/polkit/org.octopi.pacmanhelper.service" "${pkgdir}/usr/share/dbus-1/system-services/org.octopi.pacmanhelper.service"

  # Octopi notifier
  install -D -m755 "${srcdir}/${_basename}-${pkgver}/notifier/bin/octopi-notifier" "${pkgdir}/usr/bin/octopi-notifier"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/octopi-notifier.desktop" "${pkgdir}/usr/share/applications/octopi-notifier.desktop"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/octopi-notifier.desktop" "${pkgdir}/etc/xdg/autostart/octopi-notifier.desktop"

  # Repoeditor
  install -D -m755 "${srcdir}/${_basename}-${pkgver}/repoeditor/bin/octopi-repoeditor" "${pkgdir}/usr/bin/octopi-repoeditor"
  install -D -m644 "${srcdir}/octopi-repoeditor.desktop" "${pkgdir}/usr/share/applications/octopi-repoeditor.desktop"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/resources/images/octopi_red.png" "${pkgdir}/usr/share/icons/octopi-repoeditor.png"

  # Cachecleaner
  install -D -m755 "${srcdir}/${_basename}-${pkgver}/cachecleaner/bin/octopi-cachecleaner" "${pkgdir}/usr/bin/octopi-cachecleaner"
  install -D -m644 "${srcdir}/${_basename}-${pkgver}/cachecleaner/octopi-cachecleaner.desktop" "${pkgdir}/usr/share/applications/octopi-cachecleaner.desktop"
}
