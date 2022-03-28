# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Stefano Capitani <stefano[at]manjaro[dot]org>
# Contributor: Helmut Stult

# Arch credits:
# Based on the file created for Arch Linux by:
# Contributor : Christian Hesse <mail@eworm.de>
# Contributor : Ronald van Haren <ronald.archlinux.org>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Keshav Amburay <(the ddoott ridikulus ddoott rat) (aatt) (gemmaeiil) (ddoott) (ccoomm)>

## "1" to enable IA32-EFI build in Arch x86_64, "0" to disable
_IA32_EFI_IN_ARCH_X64="1"

## "1" to enable EMU build, "0" to disable
_GRUB_EMU_BUILD="1"

_GRUB_INT_VER="2.06"
_GRUB_COMMIT="53c5000739db114c229fe69ec3d4b76b92441098" # git rev-parse grub-${pkgver}
_GRUB_EXTRAS_COMMIT="8a245d5c1800627af4cefa99162a89c7a46d8842"
_UNIFONT_VER="14.0.02"

[[ "${CARCH}" == "x86_64" ]] && _EFI_ARCH="x86_64"
[[ "${CARCH}" == "i686" ]] && _EFI_ARCH="i386"
[[ "${CARCH}" == 'aarch64' ]] && _EFI_ARCH='aarch64'

[[ "${CARCH}" == "x86_64" ]] && _EMU_ARCH="x86_64"
[[ "${CARCH}" == "i686" ]] && _EMU_ARCH="i386"
[[ "${CARCH}" == 'aarch64' ]] && _EMU_ARCH='aarch64'

pkgname="grub"
pkgver=2.06
pkgrel=5
pkgdesc="GNU GRand Unified Bootloader (2)"
arch=('x86_64' 'i686' 'aarch64')
url="https://www.gnu.org/software/grub/"
license=('GPL3')
backup=('etc/default/grub'
        'etc/grub.d/40_custom'
        'boot/grub/grub.cfg')
install="${pkgname}.install"
options=('!makeflags')

conflicts=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}" 'grub-legacy')
replaces=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}")
provides=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}")

makedepends=('git' 'rsync' 'xz' 'freetype2' 'ttf-dejavu' 'python' 'autogen'
             'texinfo' 'help2man' 'gettext' 'device-mapper' 'fuse2')
depends=('sh' 'xz' 'gettext' 'device-mapper')
optdepends=('freetype2: For grub-mkfont usage'
            'fuse2: For grub-mount usage'
            'dosfstools: For grub-mkrescue FAT FS and EFI support'
            'lzop: For grub-mkrescue LZO support'
            'efibootmgr: For grub-install EFI support'
            'libisoburn: Provides xorriso for generating grub rescue iso using grub-mkrescue'
            'os-prober: To detect other OSes when generating grub.cfg in BIOS systems'
            'mtools: For grub-mkrescue FAT FS support')
            
if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    makedepends+=('libusb' 'sdl')
    optdepends+=('libusb: For grub-emu USB support'
                 'sdl: For grub-emu SDL support')
fi

validpgpkeys=('E53D497F3FA42AD8C9B4D1E835A93B74E82E4209'  # Vladimir 'phcoder' Serbinenko <phcoder@gmail.com>
              'BE5C23209ACDDACEB20DB0A28C8189F1988C2166'  # Daniel Kiper <dkiper@net-space.pl>
              '95D2E9AB8740D8046387FD151A09227B1F435A33') # Paul Hardy <unifoundry@unifoundry.com>            
            
source=("git+https://git.savannah.gnu.org/git/grub.git#tag=$_GRUB_COMMIT?signed"
        "git+https://git.savannah.gnu.org/git/grub-extras.git#commit=$_GRUB_EXTRAS_COMMIT"
        'git+https://git.savannah.gnu.org/git/gnulib.git'
        "https://ftp.gnu.org/gnu/unifont/unifont-${_UNIFONT_VER}/unifont-${_UNIFONT_VER}.bdf.gz"{,.sig}
        'grub-export-path.patch'
        'grub-add-GRUB_COLOR_variables.patch'
        'grub-manjaro-modifications.patch'
        'grub-use-efivarfs.patch'
        '0001-grub-maybe_quiet.patch'
        '0002-grub-gettext_quiet.patch'
        '0003-grub-quick-boot.patch'
        'background.png'
        'grub.default'
        'sbat.csv'
        'grub.cfg'
        'update-grub'
        'grub-set-bootflag'
        "${pkgname}.hook")
        
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            '5b314364d23143755a4b11b641a953c07837f48fefcc7454318e334265e4974b'
            'SKIP'
            '63c611189a60d68c6ae094f2ced91ac576b3921b7fd2e75a551c2dc6baefc35e'
            '4f91fda4262115a51fd8fdd7375160b8308b504b31bd6f1be6d2048d5e4a6ad2'
            '58ff142b93bfdc9375b4137607b2539a6db85b4a2bd39b063aaa37ced4d84182'
            '20b2b6e7f501596b5cce6ffa05906980427f760c03d308d0e045cf2ecf47bb0e'
            '4a0a90ae29c97b395c0610f6d78f3d39d57a7a4b41647ace9bcce4b864e19497'
            '39d7843dfe1e10ead912a81be370813b8621794a7967b3cc5e4d4188b5bf7264'
            '4cae03685c238a60169f1134165ff010faebddb5b3218d92d32e0b6729b27656'
            '01264c247283b7bbdef65d7646541c022440ddaf54f8eaf5aeb3a02eb98b4dd8'
            'c9a22df3e437599851e3c3e5725b853e8cd36728ae8fce8af5e693f4ce7c8e44'
            '89bbfe11cec0a07f5b0f170cde35abcc4cbf16d8db7b4920435525f71527fc10'
            '7fc95d49c0febe98a76e56b606a280565cb736580adecf163bc6b5aca8e7cbd8'
            'a6a3e6a7c2380aff66b6096d478aed790c927ceed551ce52c0c454191eb4e3aa'
            '2eb199f510340cf8d190ba2fa80d5bdcf1e2e7ca53e8011af2ee62ea3b8dd03b'
            'a97ddf6694fa5070463a2d3f997205436a63fbe125071dd1bef0d59999adff70')
            
_backports=(
	# fs/xfs: Fix unreadable filesystem with v4 superblock
	'a4b495520e4dc41a896a8b916a64eda9970c50ea'

	# fs/btrfs: Use full btrfs bootloader area
	'b0f06a81c6f31b6fa20be67a96b6683bba8210c9'
)

_configure_options=(
	FREETYPE="pkg-config freetype2"
	BUILD_FREETYPE="pkg-config freetype2"
	--enable-mm-debug
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

	# https://github.com/calamares/calamares/issues/918
	echo "Use efivarfs modules"
	patch -Np1 -i "${srcdir}/grub-use-efivarfs.patch"

	echo "Patch to export $PATH"
	patch -Np1 -i "${srcdir}/grub-export-path.patch"
    
	echo "Patch to enable GRUB_COLOR_* variables in grub-mkconfig"
	## Based on http://lists.gnu.org/archive/html/grub-devel/2012-02/msg00021.html
	patch -Np1 -i "${srcdir}/grub-add-GRUB_COLOR_variables.patch"
	
	echo "Patch to include Manjaro Linux Modifications"
	patch -Np1 -i "${srcdir}/grub-manjaro-modifications.patch"
	
	echo "Add Ubuntu patches"
	patch -Np1 -i "${srcdir}/0001-grub-maybe_quiet.patch"
	patch -Np1 -i "${srcdir}/0002-grub-gettext_quiet.patch"
	patch -Np1 -i "${srcdir}/0003-grub-quick-boot.patch"

	echo "Fix DejaVuSans.ttf location so that grub-mkfont can create *.pf2 files for starfield theme..."
	sed 's|/usr/share/fonts/dejavu|/usr/share/fonts/dejavu /usr/share/fonts/TTF|g' -i "configure.ac"

	echo "Fix mkinitcpio 'rw' FS#36275..."
	sed 's| ro | rw |g' -i "util/grub.d/10_linux.in"

	echo "Fix OS naming FS#33393..."
	sed 's|GNU/Linux|Linux|' -i "util/grub.d/10_linux.in"

	echo "Bump Version to ${pkgver}~${pkgrel}~manjaro"
	sed -i -e "s|${_GRUB_INT_VER}|${pkgver}~${pkgrel}~manjaro|g" "configure.ac"

	echo "Pull in latest language files..."
	./linguas.sh

	echo "Avoid problem with unifont during compile of grub..."
	# http://savannah.gnu.org/bugs/?40330 and https://bugs.archlinux.org/task/37847
	gzip -cd "${srcdir}/unifont-${_UNIFONT_VER}.bdf.gz" > "unifont.bdf"    

	# Remove lua module from grub-extras as it is incompatible with changes to grub_file_open   
	# http://git.savannah.gnu.org/cgit/grub.git/commit/?id=ca0a4f689a02c2c5a5e385f874aaaa38e151564e
	# rm -rf "$srcdir"/grub-extras/lua

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

	echo "Add the grub-extra sources for bios build..."
	install -d "${srcdir}/grub-bios/grub-extras"
	cp -r "${srcdir}/grub-extras/915resolution" \
		"${srcdir}/grub-bios/grub-extras/915resolution"
	export GRUB_CONTRIB="${srcdir}/grub-bios/grub-extras/"

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

	echo "Install grub.cfg for backup array"
	install -D -m0644 "${srcdir}/grub.cfg" "${pkgdir}/boot/grub/grub.cfg"

	echo "Install update-grub"
	install -Dm755 "${srcdir}/update-grub" "${pkgdir}/usr/bin/update-grub"

	echo "Install grub background"
	install -Dm644 "${srcdir}/background.png" "${pkgdir}/usr/share/grub/background.png"	

	echo "Install /etc/default/grub (used by grub-mkconfig)"
	install -D -m0644 "$srcdir"/grub.default "$pkgdir"/etc/default/grub

	echo "Install 99-${pkgname}.hook"
	install -D -m644 "${srcdir}/${pkgname}.hook" "${pkgdir}/usr/share/libalpm/hooks/99-${pkgname}.hook"

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

	sed -e "s/%PKGVER%/${pkgver}/" < "${srcdir}/sbat.csv" > "${pkgdir}/usr/share/grub/sbat.csv"
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

package() {
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

	# Don't overwrite /usr/share/info/dir
	rm "$pkgdir/usr/share/info/dir"
}
