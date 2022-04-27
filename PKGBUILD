# This file is part of BlackArch Linux ( https://www.blackarch.org/ ).
# See COPYING for license details.

_pkgname=V3n0M-Scanner
pkgname=v3n0m
pkgver=486.2e16dff
pkgrel=1
groups=('blackarch' 'blackarch-scanner' 'blackarch-webapp' 'blackarch-recon')
pkgdesc='Offensive Security Tool for Vulnerability Scanning & Pentesting'
arch=('any')
url='https://github.com/v3n0m-Scanner/V3n0M-Scanner'
license=('GPL3')
depends=('python' 'python-httplib2' 'python-aiohttp' 'python-asyncio'
         'python-dnslib' 'python-dnspython' 'python-multidict' 'python-requests'
         'python-pysocks' 'python-tqdm' 'python-yarl' 'python-argparse'
         'python-beautifulsoup4')
makedepends=('git' 'curl' 'python-poetry')
source=('git+https://github.com/v3n0m-Scanner/V3n0M-Scanner.git')
sha1sums=('SKIP')

pkgver() {
  cd $_pkgname
  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

package() {
  cd $_pkgname
  mkdir -p "$pkgdir/usr/bin"
  mkdir -p "$pkgdir/usr/share/v3n0m"
  cp -a src/* "$pkgdir/usr/share/v3n0m"
  install -Dm 644 -t "$pkgdir/usr/share/doc/v3n0m/" README.md
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/v3n0m/LICENSE"
  install -Dm 644 "src/desktop-menu/v3n0m.ico" \
    "$pkgdir/usr/share/icons/v3n0m.ico"
  install -Dm644 "src/desktop-menu/v3n0m.desktop" \
    "$pkgdir/usr/share/applications/v3n0m.desktop"
  curl -sSL https://install.python-poetry.org | python3 -
  poetry install

  cat > "$pkgdir/usr/bin/v3n0m" << EOF
#!/bin/sh
cd /usr/share/v3n0m
exec python v3n0m.py "\$@"
EOF

  chmod +x "$pkgdir/usr/bin/v3n0m"
}
