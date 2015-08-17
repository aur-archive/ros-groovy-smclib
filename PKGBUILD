pkgdesc="ROS - State Machine Compiler (SMC)"
url='http://www.ros.org/'

pkgname='ros-groovy-smclib'
pkgver='1.7.10'
arch=('i686' 'x86_64')
pkgrel=1
license=('Mozilla Public License Version 1.1')
makedepends=('ros-build-tools')

depends=(ros-groovy-catkin)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/smclib ]; then
    cd ${srcdir}/smclib
    git fetch origin --tags
    git reset --hard release/smclib/${pkgver}
  else
    git clone -b release/smclib/${pkgver} git://github.com/ros-gbp/bond_core-release.git ${srcdir}/smclib
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/smclib
  cmake ${srcdir}/smclib -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
