# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Stefano Capitani <stefano[at]manjaro[dot]org>
# Contributor: Helmut Stult
# Contributor: Christian Hesse <mail@eworm.de>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Ronald van Haren <ronald.archlinux.org>
# Contributor: Keshav Amburay <(the ddoott ridikulus ddoott rat) (aatt) (gemmaeiil) (ddoott) (ccoomm)>

## "1" to enable IA32-EFI build in Arch x86_64, "0" to disable
_IA32_EFI_IN_ARCH_X64="1"

## "1" to enable EMU build, "0" to disable
_GRUB_EMU_BUILD="1"

[[ "${CARCH}" == 'x86_64' ]] && _EFI_ARCH='x86_64'
[[ "${CARCH}" == 'i686' ]] && _EFI_ARCH='i386'
[[ "${CARCH}" == 'aarch64' ]] && _EFI_ARCH='aarch64'

[[ "${CARCH}" == 'x86_64' ]] && _EMU_ARCH='x86_64'
[[ "${CARCH}" == 'i686' ]] && _EMU_ARCH='i386'
[[ "${CARCH}" == 'aarch64' ]] && _EMU_ARCH='aarch64'

pkgname=(
  'grub'
  'update-grub'
  'install-grub'
)
pkgbase=grub
pkgdesc='GNU GRand Unified Bootloader (2)'
_pkgver=2.12
_unifont_ver='16.0.01'
pkgver=${_pkgver/-/}
pkgrel=7
url='https://www.gnu.org/software/grub/'
arch=('x86_64' 'aarch64')
license=('GPL-3.0-or-later')
backup=(
  etc/default/grub
  etc/grub.d/40_custom
)
install="${pkgname}.install"
options=('!makeflags')
conflicts=(
  grub-bios
  grub-common
  grub-efi-${_EFI_ARCH}
  grub-emu
  grub-legacy
)
replaces=(
  grub-common
  grub-bios
  grub-emu 
  grub-efi-${_EFI_ARCH}
)
provides=(
  grub-bios
  grub-common
  grub-efi-${_EFI_ARCH}
  grub-emu
)
makedepends=(
  autogen
  device-mapper
  freetype2
  fuse3
  gettext
  git
  help2man
  python
  rsync
  texinfo
  ttf-dejavu
  xz
)
depends=(
  device-mapper
  gettext
  sh
  xz
)
optdepends=(
  'dosfstools: For grub-mkrescue FAT FS and EFI support'
  'efibootmgr: For grub-install EFI support'
  'freetype2: For grub-mkfont usage'
  'fuse3: For grub-mount usage'
  'libisoburn: Provides xorriso for generating grub rescue iso using grub-mkrescue'
  'lzop: For grub-mkrescue LZO support'
  'mtools: For grub-mkrescue FAT FS support'
  'os-prober: To detect other OSes when generating grub.cfg in BIOS systems'
  'update-grub: Script to update Grub Menu on Linux Kernel updates'
  'install-grub: Script to install Grub after package updates'
)

if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
  makedepends+=(
  libusb
  sdl
  )
  optdepends+=(
  'libusb: For grub-emu USB support'
  'sdl: For grub-emu SDL support'
  )
fi

validpgpkeys=(
  'E53D497F3FA42AD8C9B4D1E835A93B74E82E4209'  # Vladimir 'phcoder' Serbinenko <phcoder@gmail.com>
  'BE5C23209ACDDACEB20DB0A28C8189F1988C2166'  # Daniel Kiper <dkiper@net-space.pl>
  '95D2E9AB8740D8046387FD151A09227B1F435A33') # Paul Hardy <unifoundry@unifoundry.com>

source=(
  "git+https://git.savannah.gnu.org/git/grub.git#tag=grub-${_pkgver}?signed"
  'git+https://git.savannah.gnu.org/git/gnulib.git'
  "https://ftp.gnu.org/gnu/unifont/unifont-${_unifont_ver}/unifont-${_unifont_ver}.bdf.gz"{,.sig}
  '0001-00_header-add-GRUB_COLOR_-variables.patch'
  '0003-support-dropins-for-default-configuration.patch'
  'grub.default'
  'sbat.csv'
  'grub-export-path.patch'
  'grub-manjaro-modifications.patch'
  'grub-use-efivarfs.patch'
  'grub-dont-call-fwsetup-at-all.patch'
  'fgrep-is-obsolescent-using-grep-F.patch'
  '0001-grub-maybe_quiet.patch'
  '0002-grub-gettext_quiet.patch'
  '0003-grub-quick-boot.patch'
  'background.png'
  'update-grub'
  'install-grub'
  'install-grub.conf'
  'grub-set-bootflag'
  'update-grub.hook'
  'install-grub.hook'
)
b2sums=('a6cec7271c3ea54a99f02ee6bc0a5825c8be657af68ba9a32b39a5fe8bcb571fb1ba39210426f6bf6a48d913e6e00df37dc2123ea1b39330f4c47bd9dbac9ae3'
        'SKIP'
        '9f306564a63961f3a9f7a45f3f3363b1cc44a1651c3fb858ca4e87cdad79668f9aaa4b2989f91032cd614e37a98e5ca5eda2e2b0315d99deab6d0732b6f57a0d'
        'SKIP'
        '992c71790785304c28fbaf0dba21dab3e283b199509f0e7e1aa0df08126da75e15b6626c3638279ff2ecaa59b925096d7dbd67d6a53cebd0ce4326ff3719d25b'
        'a7820bfe9bddc34af49de63222b3d2a9788367083e29db13b33120269adbfa1619ac421d8597f662f756592889f5cc5538544a17d9936d1420bd5742282c710c'
        '441bc2a47606a7f0853c571dbf578040c415bc4bd088bc645c1d6d930e552184af707a7cc677eaf92763e34eb455de50bd6fda9dd7de5be87ccdd35cea03df7c'
        'b21e36cee8a8d1cb62f30e06bfccb29ca589ff4a8fbd8f07fbe3342f25ee6a141a5e92c36387752b9bbc76c2ff32d5f1dbf839af8e56ff706bfe752f2e9dd9f5'
        '71e77b75b4f88554aabfcd5da2fcd0e150dbc199ec1779e458ee935663a7080002069a4944cb22e01a9a0af3a6434fc312db7e03888fe23c2156d25f2ba96c0a'
        '70384cd6f8af0a717b45033ae7fb1052ac43ac2698874be04da4e7bfa2c3315e8fd45a6a03371320d57bc75093ced19a863fa67abc9355ed820e65a31fec4dc8'
        'c316a8c52747a61d7b8a612b545491df9c4ba259bcfa8f923705298104eee4c4dcbdcb1d9b3473e355adab9538c4ebd4703cea63cabd6046f9887a54bd7853fb'
        'e1fdd23b992ac48a532f54e91cd77bdd636f938a9eba6bef7fd863a8cd3f5a9bc0d77122a86dc4253d3b1958ade1ea2756cbb79571794c8efdaa97c501cde3c7'
        'bd2c2a833370007e284a9799765502cf599f141207cab33548040f611c8bf16c3326ed7f7f39bb9ebdd7ededf732aae3d933bb03e7fefd5d85af08e5eead4c4b'
        'f32cf6a10416cc9cdc6c2461548b64c1a4ef240f0d52d8d2c4e7f86681d638cdc179b24e39a7f503462b9bd5190a88de7c59cc76f006eb87cd67d9da67b4f8f5'
        'd6504a70932bbea9175acafbe0e2ccc794ba3e6ef3e6e94fa05eb51caeb9373d334a9bd15649881694495e448133ac590e668a03f65fc195be4e2d622978eb93'
        '71e13690f5fa1fbe18928677b47c99a09ae333a0616eb917766f075129f2d51ad31969cd9ec1cd6bb664ab0ffae332d2400079453d9fd1ac69586abd15892e37'
        'b9530aeea084a0bbe0feedcdb9363b9933fab30f90337a79a9e2a535a2a084cbbf6458483a52b749a032858f8dd7b185e88f8fa659081886ef706eea456fc22d'
        '8b93a9564443d1509235c712e82a9aeb1d824df445eccd94f8c5f4d9050e3b1d89edefbc060b79d7ec029a2f53b19d8f31d3a82c7b8f13e8ca109751557b8b03'
        '03ddf64cebc328bd7eb7cac2ffee3e85cd91bf5138b037d775119728da0d8143e9e6a253e620747988995482971f07a0baaf66c012b0d47c1a89f20de00d44b7'
        'f24e8c7d7a424cbad8e6576ec7e65b9551f7c6b4957f7a25160193afa2681e4bdd1c4651aa8a3b29937927d95daa12f38c85e0bd7491a77dc2a6673ab2838224'
        '910ad34fcbc09bd89730bd763839d60dfc2724baf5ab91c5aa8fa9bfe8e67fc90acc863e4b21d77edb2431da801d2c3ddbb0c373717ab090c3008f4b91a6a97a'
        '842ec1c51a40f6adee2a578ff2ed083975e4f31435ce1f75191edb0731200f36d2689f0158d5da21af05293c7c62e4efc37bf1d7e6dc7211c572e746feeef7cd'
        '7d66232583d30bbade009b56ee733e51ae38ae6eec870b30494e540009b0391a26217a2c1e6980d43b2d3188e1e5e2815601dc0d3ee3b1d2ae9829820efbec28')

_backports=(
)

_reverts=(
)

_configure_options=(
  PACKAGE_VERSION="${pkgver}-${pkgrel}"
  FREETYPE="pkg-config freetype2"
  BUILD_FREETYPE="pkg-config freetype2"
  --enable-nls
  --enable-device-mapper
  --enable-cache-stats
  --enable-boot-time
  --enable-grub-mkfont
  --enable-grub-mount
  --enable-quiet-boot
  --enable-quick-boot  
  --prefix="/usr"
  --bindir="/usr/bin"
  --sbindir="/usr/bin"
  --mandir="/usr/share/man"
  --infodir="/usr/share/info"
  --datarootdir="/usr/share"
  --sysconfdir="/etc"
  --program-prefix=""
  --with-bootdir="/boot"
  --with-grubdir="grub"
  --disable-silent-rules
  --disable-werror
)

prepare() {
  cd "${srcdir}/grub/"

  echo "Apply backports..."
  local _c
  for _c in "${_backports[@]}"; do
    git log --oneline -1 "${_c}"
    git cherry-pick -n "${_c}"
  done

  echo "Apply reverts..."
  local _c
  for _c in "${_reverts[@]}"; do
    git log --oneline -1 "${_c}"
    git revert -n "${_c}"
  done

  echo "Patch to enable GRUB_COLOR_* variables in grub-mkconfig..."
  ## Based on http://lists.gnu.org/archive/html/grub-devel/2012-02/msg00021.html
  patch -Np1 -i "${srcdir}/0001-00_header-add-GRUB_COLOR_-variables.patch"

  echo "Patch to support dropins for default configuration..."
  patch -Np1 -i "${srcdir}/0003-support-dropins-for-default-configuration.patch"

  # https://github.com/calamares/calamares/issues/918
  echo "Use efivarfs modules"
  patch -Np1 -i "${srcdir}/grub-use-efivarfs.patch"

  echo 'Export $PATH'
  patch -Np1 -i "${srcdir}/grub-export-path.patch"
  
  # https://bugs.archlinux.org/task/75701
  # https://lists.gnu.org/archive/html/grub-devel/2022-08/msg00374.html
  echo "Don't call fwsetup at all"
  patch -Np1 -i "${srcdir}/grub-dont-call-fwsetup-at-all.patch"

  echo "Include Manjaro Linux Modifications"
  patch -Np1 -i "${srcdir}/grub-manjaro-modifications.patch"

  echo "fgrep is obsolescent using grep -F"
  patch -Np1 -i "${srcdir}/fgrep-is-obsolescent-using-grep-F.patch"

  echo "Add Ubuntu patches"
  echo "0001"
  patch -Np1 -i "${srcdir}/0001-grub-maybe_quiet.patch"
  echo "002"
  patch -Np1 -i "${srcdir}/0002-grub-gettext_quiet.patch"
  echo "0003"
  patch -Np1 -i "${srcdir}/0003-grub-quick-boot.patch"

  echo "Fix DejaVuSans.ttf location so that grub-mkfont can create *.pf2 files for starfield theme..."
  sed 's|/usr/share/fonts/dejavu|/usr/share/fonts/dejavu /usr/share/fonts/TTF|g' -i "configure.ac"

  echo "Fix mkinitcpio 'rw' FS#36275..."
  sed 's| ro | rw |g' -i "util/grub.d/10_linux.in"

  echo "Fix OS naming FS#33393..."
  sed 's|GNU/Linux|Linux|' -i "util/grub.d/10_linux.in"

  echo "Pull in latest language files..."
  ./linguas.sh

  echo "Avoid problem with unifont during compile of grub..."
  # http://savannah.gnu.org/bugs/?40330 and https://bugs.archlinux.org/task/37847
  gzip -cd "${srcdir}/unifont-${_unifont_ver}.bdf.gz" > "unifont.bdf"

  echo "Run bootstrap..."
  ./bootstrap \
    --gnulib-srcdir="${srcdir}/gnulib/" \
    --no-git

  echo "Make translations reproducible..."
  sed -i '1i /^PO-Revision-Date:/ d' po/*.sed
}

_build_grub-common_and_bios() {
  echo "Set ARCH dependent variables for bios build..."
  if [[ "${CARCH}" == 'x86_64' ]]; then
    _EFIEMU="--enable-efiemu"
  else
    _EFIEMU="--disable-efiemu"
  fi

  echo "Copy the source for building the bios part..."
  cp -r "${srcdir}/grub/" "${srcdir}/grub-bios/"
  cd "${srcdir}/grub-bios/"

  echo "Unset all compiler FLAGS for bios build..."
  unset CFLAGS
  unset CPPFLAGS
  unset CXXFLAGS
  unset LDFLAGS
  unset MAKEFLAGS

  echo "Run ./configure for bios build..."
  ./configure \
    --with-platform="pc" \
    --target="i386" \
    "${_EFIEMU}" \
    --enable-boot-time \
    "${_configure_options[@]}"

  if [ ! -z "${SOURCE_DATE_EPOCH}" ]; then
    echo "Make info pages reproducible..."
    touch -d "@${SOURCE_DATE_EPOCH}" $(find -name '*.texi')
  fi

  echo "Run make for bios build..."
  make
}

_build_grub-efi() {
  echo "Copy the source for building the ${_EFI_ARCH} efi part..."
  cp -r "${srcdir}/grub/" "${srcdir}/grub-efi-${_EFI_ARCH}/"
  cd "${srcdir}/grub-efi-${_EFI_ARCH}/"

  echo "Unset all compiler FLAGS for ${_EFI_ARCH} efi build..."
  unset CFLAGS
  unset CPPFLAGS
  unset CXXFLAGS
  unset LDFLAGS
  unset MAKEFLAGS

  echo "Run ./configure for ${_EFI_ARCH} efi build..."
  ./configure \
    --with-platform="efi" \
    --target="${_EFI_ARCH}" \
    --disable-efiemu \
    --enable-boot-time \
    "${_configure_options[@]}"

  echo "Run make for ${_EFI_ARCH} efi build..."
  make
}

_build_grub-emu() {
  echo "Copy the source for building the emu part..."
  cp -r "${srcdir}/grub/" "${srcdir}/grub-emu/"
  cd "${srcdir}/grub-emu/"

  echo "Unset all compiler FLAGS for emu build..."
  unset CFLAGS
  unset CPPFLAGS
  unset CXXFLAGS
  unset LDFLAGS
  unset MAKEFLAGS

  echo "Run ./configure for emu build..."
  ./configure \
    --with-platform="emu" \
    --target="${_EMU_ARCH}" \
    --enable-grub-emu-usb=no \
    --enable-grub-emu-sdl=no \
    --disable-grub-emu-pci \
    "${_configure_options[@]}"

  echo "Run make for emu build..."
  make
}

build() {
  cd "${srcdir}/grub/"

  echo "Build grub bios stuff..."
  _build_grub-common_and_bios

  echo "Build grub ${_EFI_ARCH} efi stuff..."
  _build_grub-efi

  if [[ "${CARCH}" == "x86_64" ]] && [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
    echo "Build grub i386 efi stuff..."
    _EFI_ARCH="i386" _build_grub-efi
  fi

  if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    echo "Build grub emu stuff..."
    _build_grub-emu
  fi
}

_package_grub-common_and_bios() {
  cd "${srcdir}/grub-bios/"

  echo "Run make install for bios build..."
  make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

  echo "Remove gdb debugging related files for bios build..."
  rm -f "${pkgdir}/usr/lib/grub/i386-pc"/*.module || true
  rm -f "${pkgdir}/usr/lib/grub/i386-pc"/*.image || true
  rm -f "${pkgdir}/usr/lib/grub/i386-pc"/{kernel.exec,gdb_grub,gmodule.pl} || true

  echo "Install grub background"
  install -Dm644 "${srcdir}/background.png" "${pkgdir}/usr/share/grub/background.png"  

  echo "Install /etc/default/grub (used by grub-mkconfig)"
  install -D -m0644 "$srcdir"/grub.default "$pkgdir"/etc/default/grub

  # workaround for quiet fsck
  install -D -m755 "${srcdir}/grub-set-bootflag" "${pkgdir}/usr/bin/grub-set-bootflag"
}

_package_grub-efi() {
  cd "${srcdir}/grub-efi-${_EFI_ARCH}/"

  echo "Run make install for ${_EFI_ARCH} efi build..."
  make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

  echo "Remove gdb debugging related files for ${_EFI_ARCH} efi build..."
  rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.module || true
  rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.image || true
  rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/{kernel.exec,gdb_grub,gmodule.pl} || true

  sed -e "s/%PKGVER%/${pkgver}-${pkgrel}/" < "${srcdir}/sbat.csv" > "${pkgdir}/usr/share/grub/sbat.csv"
}

_package_grub-emu() {
  cd "${srcdir}/grub-emu/"

  echo "Run make install for emu build..."
  make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

  echo "Remove gdb debugging related files for emu build..."
  rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.module || true
  rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.image || true
  rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/{kernel.exec,gdb_grub,gmodule.pl} || true
}

package_grub() {
  install="${pkgname}.install"

  cd "${srcdir}/grub/"

  echo "Package grub ${_EFI_ARCH} efi stuff..."
  _package_grub-efi

  if [[ "${CARCH}" == "x86_64" ]] && [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
    echo "Package grub i386 efi stuff..."
    _EFI_ARCH="i386" _package_grub-efi
  fi

  if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    echo "Package grub emu stuff..."
    _package_grub-emu
  fi

  echo "Package grub bios stuff..."
  _package_grub-common_and_bios
}

package_update-grub() {
  pkgdesc="GNU Grub (2) Update Menu Script"
  depends=(grub)
  optdepends=()
  provides=()
  conflicts=('grub-update')
  replaces=('grub-update')
  backup=()
  echo "Install update-grub"
  install -Dm755 "${srcdir}/update-grub" "${pkgdir}/usr/bin/update-grub"
  echo "Install 99-update-grub.hook"
  install -D -m644 "${srcdir}/update-grub.hook" "${pkgdir}/usr/share/libalpm/hooks/99-update-grub.hook"
}

package_install-grub() {
  pkgdesc="GNU Grub (2) Install Script on Updates"
  depends=(coreutils efibootmgr gawk grep grub)
  optdepends=()
  provides=()
  conflicts=()
  replaces=()
  backup=('etc/install-grub.conf')
  echo "Install install-grub"
  install -Dm755 "${srcdir}/install-grub" "${pkgdir}/usr/bin/install-grub"
  echo "Install install-grub.conf"
  install -Dm644 "${srcdir}/install-grub.conf" "${pkgdir}/etc/install-grub.conf"
  echo "Install 98-install-grub.hook"
  install -Dm644 "${srcdir}/install-grub.hook" "${pkgdir}/usr/share/libalpm/hooks/98-install-grub.hook"
}
