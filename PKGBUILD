# Maintainer: robertfoster
# Contributor: zozs

pkg=linux-sgx-driver
pkgname=$pkg-dkms-git
pkgver=2.1.r0.g03e9152
pkgrel=1
pkgdesc="Intel® SGX Linux module - dkms"
arch=('i686' 'x86_64')
url="https://01.org/intel-softwareguard-extensions"
license=('GPL2')
depends=('dkms')
optdepends=('linux-headers: Build the module for Arch kernel'
            'linux-lts-headers: Build the module for LTS Arch kernel')
makedepends=('linux-headers>=4.12' 'linux>=4.12')
source=("$pkg::git+https://github.com/01org/linux-sgx-driver.git#branch=sgx2"
	dkms.conf
	makefile-no-optimization.patch)

pkgver() {
  cd $srcdir/$pkg
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g' | cut -c 12-
}

prepare() {
  patch -p1 -i makefile-no-optimization.patch
}

package() {
  installDir="$pkgdir/usr/src/$pkg-$pkgver"

  install -dm755 "$installDir"

# Copy dkms .conf
  install -Dm644 ../dkms.conf "$installDir/dkms.conf"

# Set name and version
  sed -e "s/@PKG@/${pkg}/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "$pkgdir/usr/src/$pkg-$pkgver/dkms.conf"

# Copy sources
  cd $srcdir/$pkg

  for d in `find . -type d`
    do
      install -dm755  "${installDir}/$d"
    done
  for f in `find . -type f ! -name 'README.md' ! -name '.gitignore'`
    do
      install -m644 "$f" "${installDir}/$f"
    done
}

sha256sums=('SKIP'
            'e2fbb933feb550fa616ed3df4ddd6942447f262f9efe02092bf58cb0f6ed4b70'
            '6679c88a969da5f09b324a37dd0cb1f9c8e4b4f3cd261c7103f22664c247b4c5')
