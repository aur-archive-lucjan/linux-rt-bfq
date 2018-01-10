# Maintainer: Piotr Gorski <lucjan.lucjanov@gmail.com>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Thomas Baechler <thomas@archlinux.org>

### BUILD OPTIONS
# Set these variables to ANYTHING that is not null to enable them

### Use tentative patches from https://groups.google.com/forum/#!forum/bfq-iosched
### Thx to Tom 'monotykamary' Nguyen
_use_tentative_patches=

### Use patches from https://marc.info/?l=linux-block&m=150797307912556&w=1
_use_blk_mq_patches=

### Use disable writeback throttling: https://marc.info/?l=linux-block&m=150486424501778&w=2
_use_lucamiccio_patch=

### Tweak kernel options prior to a build via nconfig
_makenconfig=

### Tweak kernel options prior to a build via menuconfig
_makemenuconfig=

### Tweak kernel options prior to a build via xconfig
_makexconfig=

### Tweak kernel options prior to a build via gconfig
_makegconfig=

### Running with a 1000 HZ tick rate 
_1k_HZ_ticks=y

# NUMA is optimized for multi-socket motherboards.
# A single multi-core CPU actually runs slower with NUMA enabled.
# See, https://bugs.archlinux.org/task/31187
_NUMAdisable=y

# Compile ONLY probed modules
# As of mainline 2.6.32, running with this option will only build the modules
# that you currently have probed in your system VASTLY reducing the number of
# modules built and the build time to do it.
#
# WARNING - ALL modules must be probed BEFORE you begin making the pkg!
#
# To keep track of which modules are needed for your specific system/hardware,
# give module_db script a try: https://aur.archlinux.org/packages/modprobed-db
# This PKGBUILD will call it directly to probe all the modules you have logged!
#
# More at this wiki page ---> https://wiki.archlinux.org/index.php/Modprobed_db
_localmodcfg=

# Use the current kernel's .config file
# Enabling this option will use the .config of the RUNNING kernel rather than
# the ARCH defaults. Useful when the package gets updated and you already went
# through the trouble of customizing your config options.  NOT recommended when
# a new kernel is released, but again, convenient for package bumps.
_use_current=

### Enable MQ scheduling 
_mq_enable=

### Do not edit below this line unless you know what you're doing

pkgbase=linux-rt-bfq
# pkgname=('linux-rt-bfq' 'linux-rt-bfq-headers' 'linux-rt-bfq-docs')
_srcname=linux-4.14
_pkgver=4.14.12
_rtver=10
_rtpatchver=rt${_rtver}
_srcpatch="${_pkgver##*\.*\.}"
pkgver=${_pkgver}.${_rtver}
pkgrel=3
arch=('x86_64')
url="https://github.com/Algodev-github/bfq-mq/"
license=('GPL2')
options=('!strip')
makedepends=('kmod' 'inetutils' 'bc' 'libelf')
_bfq_sq_mq_ver='20180110'
_bfq_sq_mq_patch="4.14-bfq-sq-mq-git-${_bfq_sq_mq_ver}.patch"
#_lucjanpath="https://raw.githubusercontent.com/sirlucjan/kernel-patches/master/4.14"
_lucjanpath="https://gitlab.com/sirlucjan/kernel-patches/raw/master/4.14"
_gcc_path="https://raw.githubusercontent.com/sirlucjan/kernel_gcc_patch/master"
_gcc_patch="enable_additional_cpu_optimizations_for_gcc_v4.9+_kernel_v4.13+.patch"

source=("https://www.kernel.org/pub/linux/kernel/v4.x/${_srcname}.tar.xz"
        "https://www.kernel.org/pub/linux/kernel/v4.x/${_srcname}.tar.sign"
        "https://www.kernel.org/pub/linux/kernel/v4.x/patch-${_pkgver}.xz"
        "https://www.kernel.org/pub/linux/kernel/v4.x/patch-${_pkgver}.sign"
        "http://www.kernel.org/pub/linux/kernel/projects/rt/4.14/patch-${_pkgver}-${_rtpatchver}.patch.xz"
        "http://www.kernel.org/pub/linux/kernel/projects/rt/4.14/patch-${_pkgver}-${_rtpatchver}.patch.sign"
        "${_lucjanpath}/${_bfq_sq_mq_patch}"
        "${_lucjanpath}/0009-bfq-sq-mq-fix-patching-error-with-20180109.patch"
        "${_lucjanpath}/blk-mq-v10/0051-blk-mq-sched-move-actual-dispatching-into-one-helper.patch"
        "${_lucjanpath}/blk-mq-v10/0052-blk-mq-sbitmap-introduce__sbitmap_for_each_set().patch"
        "${_lucjanpath}/blk-mq-v10/0053-blk-mq-block-kyber-check-if-there-is-request-in-ctx-in-kyber_has_work().patch"
        "${_lucjanpath}/blk-mq-v10/0054-blk-mq-introduce-get_budget-and-put_budget-in-blk_mq_ops.patch"
        "${_lucjanpath}/blk-mq-v10/0055-blk-mq-sched-improve-dispatching-from-sw-queue.patch"
        "${_lucjanpath}/blk-mq-v10/0056-blk-mq-SCSI-allow-to-pass-null-rq-to-scsi_prep_state_check().patch"
        "${_lucjanpath}/blk-mq-v10/0057-blk-mq-SCSI-implement-get-budget-and-put_budget-for-blk-mq.patch"
        "${_lucjanpath}/0100-Check-presence-on-tree-of-every-entity-after-every-a.patch"
        "${_lucjanpath}/0300-Disable-writeback-throttling.patch"
        "${_gcc_path}/${_gcc_patch}"
        'fix-race-in-PRT-wait-for-completion-simple-wait-code_Nvidia-RT-160319.patch'
         # the main kernel config files
        'config'
         # pacman hook for depmod
        '60-linux.hook'
         # pacman hook for initramfs regeneration
        '90-linux.hook'
         # pacman hook for remove initramfs
        '99-linux.hook'
         # standard config files for mkinitcpio ramdisk
        'linux.preset'
        '0001-add-sysctl-to-disallow-unprivileged-CLONE_NEWUSER-by.patch'
        '0002-e1000e-Fix-e1000_check_for_copper_link_ich8lan-retur.patch'
        '0003-dccp-CVE-2017-8824-use-after-free-in-DCCP-code.patch'
        '0004-xfrm-Fix-stack-out-of-bounds-read-on-socket-policy-l.patch'
        '0005-cgroup-fix-css_task_iter-crash-on-CSS_TASK_ITER_PROC.patch'
        '0006-drm-i915-edp-Only-use-the-alternate-fixed-mode-if-it.patch')
        
_kernelname=${pkgbase#linux} 

prepare() {
    cd ${_srcname}

    ### Add upstream patch
        msg "Add upstream patch"
        patch -p1 -i ../patch-${_pkgver}
    
    ### Add rt patch
        msg "Add rt patch"
        patch -Np1 -i ../patch-${_pkgver}-${_rtpatchver}.patch
    
    ### Disable USER_NS for non-root users by default
        msg "Disable USER_NS for non-root users by default"
        patch -Np1 -i ../0001-add-sysctl-to-disallow-unprivileged-CLONE_NEWUSER-by.patch
  
    ### Fix https://bugs.archlinux.org/task/56575
        msg "Fix #56575" 
        patch -Np1 -i ../0002-e1000e-Fix-e1000_check_for_copper_link_ich8lan-retur.patch

    ### Fix https://nvd.nist.gov/vuln/detail/CVE-2017-8824
        msg "Fix CVE-2017-8824"
        patch -Np1 -i ../0003-dccp-CVE-2017-8824-use-after-free-in-DCCP-code.patch
  
    ### Fix https://bugs.archlinux.org/task/56605
        msg "Fix #56605"
        patch -Np1 -i ../0004-xfrm-Fix-stack-out-of-bounds-read-on-socket-policy-l.patch
  
    ### Fix https://bugs.archlinux.org/task/56846
        msg "Fix #56846"
        patch -Np1 -i ../0005-cgroup-fix-css_task_iter-crash-on-CSS_TASK_ITER_PROC.patch
    
    ### Fix https://bugs.archlinux.org/task/56711
        msg "Fix #56711"
        patch -Np1 -i ../0006-drm-i915-edp-Only-use-the-alternate-fixed-mode-if-it.patch
    
    ### A patch to fix a problem that ought to be fixed in the NVIDIA source code.
    # Stops X from hanging on certain NVIDIA cards
        msg "Fix-race-in-PRT-wait-for-completion-simple-wait-code_Nvidia-RT.patch"
        patch -p1 -i ../fix-race-in-PRT-wait-for-completion-simple-wait-code_Nvidia-RT-160319.patch
            
    ### Patch source with BFQ-SQ-MQ
        msg "Fix patching with 20180109"
        patch -Np1 -i ../0009-bfq-sq-mq-fix-patching-error-with-20180109.patch
        msg "Fix naming schema in BFQ-SQ-MQ patch"
        sed -i -e "s|PATCHLEVEL = 15|PATCHLEVEL = 14|g" \
            -i -e "s|SUBLEVEL = 0|SUBLEVEL = ${_srcpatch}|g" \
            -i -e "s|EXTRAVERSION = -rc7|EXTRAVERSION =|g" \
            -i -e "s|EXTRAVERSION = -bfq-rc7|EXTRAVERSION =|g" \
            -i -e "s|EXTRAVERSION = -bfq-mq-rc7|EXTRAVERSION =|g" \
            -i -e "s|NAME = Fearless Coyote|NAME = Petit Gorille|g" ../${_bfq_sq_mq_patch}
        msg "Patching source with BFQ-SQ-MQ patches"
        patch -Np1 -i ../${_bfq_sq_mq_patch}
        
    ### Patches related to BUG_ON(entity->tree && entity->tree != &st->active) in __bfq_requeue_entity();
        if [ -n "$_use_tentative_patches" ]; then
        msg "Apply tentative patches"
        for p in "${srcdir}"/0100*.patch*; do 
        msg " $p"
        patch -Np1 -i "$p"; done
        fi
        
    ### Use patches from https://marc.info/?l=linux-block&m=150797307912556&w=1
        if [ -n "$_use_blk_mq_patches" ]; then
        msg "Apply blk-mq patches"
        for p in "${srcdir}"/*-blk-mq*.patch*; do 
        msg " $p" 
        patch -Np1 -i "$p"; done
        fi     
    
    ### Patch from https://marc.info/?l=linux-block&m=150486424501778&w=2
        if [ -n "$_use_lucamiccio_patch" ]; then
        msg "Apply Luca Miccio patch"
        for p in "${srcdir}"/0300*.patch*; do 
        msg " $p" 
        patch -Np1 -i "$p"; done
        fi
    
    ### Patch source to enable more gcc CPU optimizatons via the make nconfig
        msg "Patching source with gcc patch to enable more cpus types"
	patch -Np1 -i ../${_gcc_patch}
	
    ### Fix https://www.spinics.net/lists/stable/msg207374.html
        msg "Fix execvp: ./sync-check.sh error"
        chmod +x tools/objtool/sync-check.sh
    
    ### Clean tree and copy ARCH config over
	msg "Running make mrproper to clean source tree"
	make mrproper

	cp -Tf ../config .config
        
    ### Optionally use running kernel's config
	# code originally by nous; http://aur.archlinux.org/packages.php?ID=40191
	if [ -n "$_use_current" ]; then
		if [[ -s /proc/config.gz ]]; then
			msg "Extracting config from /proc/config.gz..."
			# modprobe configs
			zcat /proc/config.gz > ./.config
		else
			warning "You kernel was not compiled with IKCONFIG_PROC!"
			warning "You cannot read the current config!"
			warning "Aborting!"
			exit
		fi
	fi    
        
    ### Optionally set tickrate to 1000 
	if [ -n "$_1k_HZ_ticks" ]; then
		msg "Setting tick rate to 1k..."
		sed -i -e 's/^CONFIG_HZ_300=y/# CONFIG_HZ_300 is not set/' \
			-i -e 's/^# CONFIG_HZ_1000 is not set/CONFIG_HZ_1000=y/' \
			-i -e 's/^CONFIG_HZ=300/CONFIG_HZ=1000/' .config
	fi
	
    ### Enable MQ scheduling
        if [ -n "$_mq_enable" ]; then
            msg "Enable MQ scheduling..."
            sed -i -e s'/^# CONFIG_SCSI_MQ_DEFAULT is not set/CONFIG_SCSI_MQ_DEFAULT=y/' \
                -i -e s'/^# CONFIG_DM_MQ_DEFAULT is not set/CONFIG_DM_MQ_DEFAULT=y/' ./.config
        fi
   
	if [ "${_kernelname}" != "" ]; then
		sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"${_kernelname}\"|g" ./.config
		sed -i "s|CONFIG_LOCALVERSION_AUTO=.*|CONFIG_LOCALVERSION_AUTO=n|" ./.config
	fi

    ### Optionally disable NUMA for 64-bit kernels only
        # (x86 kernels do not support NUMA)
        if [ -n "$_NUMAdisable" ]; then
            msg "Disabling NUMA from kernel config..."
            sed -i -e 's/CONFIG_NUMA=y/# CONFIG_NUMA is not set/' \
                -i -e '/CONFIG_AMD_NUMA=y/d' \
                -i -e '/CONFIG_X86_64_ACPI_NUMA=y/d' \
                -i -e '/CONFIG_NODES_SPAN_OTHER_NODES=y/d' \
                -i -e '/# CONFIG_NUMA_EMU is not set/d' \
                -i -e '/CONFIG_NODES_SHIFT=6/d' \
                -i -e '/CONFIG_NEED_MULTIPLE_NODES=y/d' \
                -i -e '/# CONFIG_MOVABLE_NODE is not set/d' \
                -i -e '/CONFIG_USE_PERCPU_NUMA_NODE_ID=y/d' \
                -i -e '/CONFIG_ACPI_NUMA=y/d' ./.config
        fi

	### Set extraversion to pkgrel
	sed -ri "s|^(EXTRAVERSION =).*|\1 -${pkgrel}|" Makefile

	### Don't run depmod on 'make install'. We'll do this ourselves in packaging
	sed -i '2iexit 0' scripts/depmod.sh

	### Get kernel version
	msg "Running make prepare for you to enable patched options of your choosing"
	make prepare

	### Optionally load needed modules for the make localmodconfig
	# See https://aur.archlinux.org/packages/modprobed-db
		if [ -n "$_localmodcfg" ]; then
		msg "If you have modprobe-db installed, running it in recall mode now"
		if [ -e /usr/bin/modprobed-db ]; then
			[[ -x /usr/bin/sudo ]] || {
                        echo "Cannot call modprobe with sudo. Install sudo and configure it to work with this user."
                        exit 1; }
			sudo /usr/bin/modprobed-db recall
		fi
		msg "Running Steven Rostedt's make localmodconfig now"
		make localmodconfig
	fi

	### Running make nconfig
	
	[[ -z "$_makenconfig" ]] ||  make nconfig
	
	### Running make menuconfig
	
	[[ -z "$_makemenuconfig" ]] || make menuconfig
	
	### Running make xconfig
	
	[[ -z "$_makexconfig" ]] || make xconfig
	
	### Running make gconfig
	
	[[ -z "$_makegconfig" ]] || make gconfig
	
	### Rewrite configuration
	yes "" | make config >/dev/null

	### Save configuration for later reuse
	cat .config > "${startdir}/config.last"
}

build() {
  cd ${_srcname}

  make ${MAKEFLAGS} LOCALVERSION= bzImage modules
}

_package() {
    pkgdesc='Linux Kernel and modules with the RT patch and the  BFQ scheduler.'
    depends=('coreutils' 'linux-firmware' 'mkinitcpio>=0.7')
    optdepends=('crda: to set the correct wireless channels of your country' 'modprobed-db: Keeps track of EVERY kernel module that has ever been probed - useful for those of us who make localmodconfig')
    backup=("etc/mkinitcpio.d/${pkgbase}.preset")
    install=linux.install

    cd ${_srcname}

    # get kernel version
    _kernver="$(make LOCALVERSION= kernelrelease)"
    _basekernel=${_kernver%%-*}
    _basekernel=${_basekernel%.*}

    mkdir -p "${pkgdir}"/{boot,usr/lib/modules}
    make LOCALVERSION= INSTALL_MOD_PATH="${pkgdir}/usr" modules_install
    cp arch/x86/boot/bzImage "${pkgdir}/boot/vmlinuz-${pkgbase}"

    # make room for external modules
    local _extramodules="extramodules-${_basekernel}${_kernelname:--ARCH}"
    ln -s "../${_extramodules}" "${pkgdir}/usr/lib/modules/${_kernver}/extramodules"

    # add real version for building modules and running depmod from hook
    echo "${_kernver}" |
        install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modules/${_extramodules}/version"

    # remove build and source links
    rm "${pkgdir}"/usr/lib/modules/${_kernver}/{source,build}

    # now we call depmod...
    depmod -b "${pkgdir}/usr" -F System.map "${_kernver}"

    # add vmlinux
    install -Dt "${pkgdir}/usr/lib/modules/${_kernver}/build" -m644 vmlinux

    # sed expression for following substitutions
    local _subst="
        s|%PKGBASE%|${pkgbase}|g
        s|%KERNVER%|${_kernver}|g
        s|%EXTRAMODULES%|${_extramodules}|g
    "

    # hack to allow specifying an initially nonexisting install file
    sed "${_subst}" "${startdir}/${install}" > "${startdir}/${install}.pkg"
    true && install=${install}.pkg

    # install mkinitcpio preset file
    sed "${_subst}" ../linux.preset |
        install -Dm644 /dev/stdin "${pkgdir}/etc/mkinitcpio.d/${pkgbase}.preset"

    # install pacman hooks
    sed "${_subst}" ../60-linux.hook |
        install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/60-${pkgbase}.hook"
    sed "${_subst}" ../90-linux.hook |
        install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/90-${pkgbase}.hook"
    sed "${_subst}" ../99-linux.hook |
        install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/99-${pkgbase}.hook"    
}

_package-headers() {
    pkgdesc='Header files and scripts to build modules for linux-rt-bfq.'
    depends=('linux-rt-bfq')

    cd ${_srcname}
    local _builddir="${pkgdir}/usr/lib/modules/${_kernver}/build"

    install -Dt "${_builddir}" -m644 Makefile .config Module.symvers
    install -Dt "${_builddir}/kernel" -m644 kernel/Makefile

    mkdir "${_builddir}/.tmp_versions"

    cp -t "${_builddir}" -a include scripts

    install -Dt "${_builddir}/arch/x86" -m644 arch/x86/Makefile
    install -Dt "${_builddir}/arch/x86/kernel" -m644 arch/x86/kernel/asm-offsets.s

    cp -t "${_builddir}/arch/x86" -a arch/x86/include

    install -Dt "${_builddir}/drivers/md" -m644 drivers/md/*.h
    install -Dt "${_builddir}/net/mac80211" -m644 net/mac80211/*.h

    # http://bugs.archlinux.org/task/9912
    install -Dt "${_builddir}/drivers/media/dvb-core" -m644 drivers/media/dvb-core/*.h

    # http://bugs.archlinux.org/task/13146
    install -Dt "${_builddir}/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

    # http://bugs.archlinux.org/task/20402
    install -Dt "${_builddir}/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
    install -Dt "${_builddir}/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
    install -Dt "${_builddir}/drivers/media/tuners" -m644 drivers/media/tuners/*.h

    # add xfs and shmem for aufs building
    mkdir -p "${_builddir}"/{fs/xfs,mm}

    # copy in Kconfig files
    find . -name Kconfig\* -exec install -Dm644 {} "${_builddir}/{}" \;

    # add objtool for external module building and enabled VALIDATION_STACK option
    install -Dt "${_builddir}/tools/objtool" tools/objtool/objtool

    # remove unneeded architectures
    local _arch
    for _arch in "${_builddir}"/arch/*/; do
        [[ ${_arch} == */x86/ ]] && continue
        rm -r "${_arch}"
    done

    # remove files already in linux-rt-bfq-docs package
    rm -r "${_builddir}/Documentation"
    
    # remove now broken symlinks
    find -L "${_builddir}" -type l -printf 'Removing %P\n' -delete

    # Fix permissions
    chmod -R u=rwX,go=rX "${_builddir}"

    # strip scripts directory
    local _binary _strip
    while read -rd '' _binary; do
        case "$(file -bi "${_binary}")" in
        *application/x-sharedlib*)  _strip="${STRIP_SHARED}"   ;; # Libraries (.so)
        *application/x-archive*)    _strip="${STRIP_STATIC}"   ;; # Libraries (.a)
        *application/x-executable*) _strip="${STRIP_BINARIES}" ;; # Binaries
        *) continue ;;
        esac
        /usr/bin/strip ${_strip} "${_binary}"
    done < <(find "${_builddir}/scripts" -type f -perm -u+w -print0 2>/dev/null)
}

_package-docs() {
    pkgdesc="Kernel hackers manual - HTML documentation that comes with the linux-rt-bfq kernel"
    depends=('linux-rt-bfq')
  
    cd ${_srcname}
    local _builddir="${pkgdir}/usr/lib/modules/${_kernver}/build"

    mkdir -p "${_builddir}"
    cp -t "${_builddir}" -a Documentation

    # Fix permissions
    chmod -R u=rwX,go=rX "${_builddir}"
}

pkgname=("${pkgbase}" "${pkgbase}-headers" "${pkgbase}-docs")
for _p in ${pkgname[@]}; do
  eval "package_${_p}() {
    $(declare -f "_package${_p#${pkgbase}}")
    _package${_p#${pkgbase}}
  }"
done

sha512sums=('77e43a02d766c3d73b7e25c4aafb2e931d6b16e870510c22cef0cdb05c3acb7952b8908ebad12b10ef982c6efbe286364b1544586e715cf38390e483927904d8'
            'SKIP'
            'b11b91503c9eb879b79cb16683204f5dbb467aac62dcfc1b025f889dc38016d990c0fd1879210226430e9f9ac6e168439b13603781188d67d213b12a334b4e5b'
            'SKIP'
            '4a89fbe2ebca6bbf3f10329e80bc6c51061d2092fe659c12cd918f11a867afb42391bc979282e7c1c252b6b257d810441fa50f1c58293eaae305816cbe416c3a'
            'SKIP'
            '485756bd18308ccc036d16ddc3693db931d545c59310525127a331b746ee99c4ec689762b39b593998279ca767df0e290405705d9632a14cc248857f32860728'
            'e1819903787241db1fc7cf4fb7682936185c73ef7ba842f59b94f2d56ef2ceab3df42344df3cb226060c09257d98e9a861bc8f7a7debc0a9f0936022022fc3ba'
            'ca6a40800668c0fcf478bd1bc555e5a496f5259739594bf83cc4963756b7a9a0a5b406e91f760d35f1bce1268c01d779fe2a7e749eccf9412e826152a5f013ef'
            '1434cc3957ef77fb83c9385a348f36ca43a73459b8995d3061143d1d15b307f944c39abc0eb109d20869c1749348d608c58cf5b92fd81ad65cad2d362e346549'
            '49c8619a96d7145e8fe77fad4394db7b24a73d94c1e01866e4a3bc5b044dbbb59c8aa2db62d72ef8460ec777d88959b545ad6373073fe3fd21016e5fc08c9f3c'
            '8d81793da14847ee521d230a3065b0c1dfd0138c28ea350754de21e2908132866e4851119f98182cf8725a92a803c31999f457a495c5079afe7d82470f5fcb63'
            '27b68107c4920baf85a5b1e1636d523399bcc1c7bce5e238ee321c666bb79f0124890577b3cba16a99d7da406015401324e8d04b91a1f73e4093473033ae237a'
            '82e624f91c6609bec6ebbc284c8413e638802d3306d6e3826524631fd3a4fdaaed9a85a366e9d3deab2d1b1638f2225a64942e754145ea30da896fc3155574eb'
            '75403516c0e64e13c66602ade9ac12fd553ec811628b4bba79686e183e12a798281566dfdbbe0ba1217ebe8ee1d294a7ca904c36d7b760bcb558ddca0cb7f260'
            '0f96fa9ad784709973b32eea82075ceb3e9dc2482df6441a4607612806f069254e63508b1b562279622394e4a1fbebef1b87af8401c0b1210d5d0de9954245c8'
            'a1ccc22354a420467fb912f822585ed4573e68f4694f02ab83d7c8e352da88be495acb3cb4c451c27ca0cf0befe5925b8734d37205bb3dfdaf86d2dedef0798f'
            '5ca7ae20245a54caa71fb570d971d6872d4e888f35c6123b93fbca16baf9a0e2500d6ec931f3906e4faecaaca9cad0d593694d9cab617efd0cb7b5fc09c0fa48'
            '86f717f596c613db3bc40624fd956ed379b8a2a20d1d99e076ae9061251fe9afba39cf536623eccd970258e124b8c2c05643e3d539f37bd910e02dc5dd498749'
            '8de599a8c9433e7e8045df4c7ec777c164fe67cc28567403da233e278a38d8c4e91a8fc347758c0f3473634dd0a422ad1737beaa9be5247bf5ff1dd2b3d59d7d'
            '7ad5be75ee422dda3b80edd2eb614d8a9181e2c8228cd68b3881e2fb95953bf2dea6cbe7900ce1013c9de89b2802574b7b24869fc5d7a95d3cc3112c4d27063a'
            '4a8b324aee4cccf3a512ad04ce1a272d14e5b05c8de90feb82075f55ea3845948d817e1b0c6f298f5816834ddd3e5ce0a0e2619866289f3c1ab8fd2f35f04f44'
            '6346b66f54652256571ef65da8e46db49a95ac5978ecd57a507c6b2a28aee70bb3ff87045ac493f54257c9965da1046a28b72cb5abb0087204d257f14b91fd74'
            '2dc6b0ba8f7dbf19d2446c5c5f1823587de89f4e28e9595937dd51a87755099656f2acec50e3e2546ea633ad1bfd1c722e0c2b91eef1d609103d8abdc0a7cbaf'
            '46447e0257b7ad5db932eb50a241d046716f21b9c12698c9d83d5f3ef52aff4ba603b79a26616347e6993dcc4ec7452aef3c0c9cf430c73955ee8e61c62194a7'
            '6f3b1efe81ac806217dd199a629f2d1ed55c6393ba1d90600cd2d2f41a865dca680e131b668265cc3e665be748295aea1b65877d737064661450d5cd089f0d96'
            'baa77972acdc1820af6ea82ae72e1dbc793bde242d77a5176ab29444c8a3e3c3670907a5e289045d1246e2dd706cdab64659f82605e2f84b30d5b3c8f3272de5'
            '096eb9bbdeacae276145fc7b28946e8f6a432f9b5159b8a33d1df00c820d8b96780cc84541c30bb75bf8d9324ecb3222c2bcd9630d5310ef1d17d6fad0f68a15'
            'cfc7ee58c22639ed6a891ad6f42b2fbe15f684d706c8026b8b0cb463a06d8446ac06cacdac47a1e1c91028bea1611ae2e5d017a7e07a5471589039f33501966b'
            'fcc40dc86dd432be76854e3c51889db488de0f1029ecc227b92c4f58c62ba928f7dc3b9515ac3ca0a08d6a0a72ca4a1a754d47c4fb274fe89f09a2a336088e7a')
            
validpgpkeys=(
              'ABAF11C65A2970B130ABE3C479BE3E4300411886' # Linus Torvalds
              '647F28654894E3BD457199BE38DBBDC86092693E' # Greg Kroah-Hartman
              '64254695FFF0AA4466CC19E67B96E8162A8CF5D1' # Sebastian Andrzej Siewior
              '5ED9A48FC54C0A22D1D0804CEBC26CDB5A56DE73' # Steven Rostedt
              'E644E2F1D45FA0B2EAA02F33109F098506FF0B14' # Thomas Gleixner
              )
