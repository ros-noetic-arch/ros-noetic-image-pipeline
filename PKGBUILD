pkgdesc="ROS - image_pipeline fills the gap between getting raw images from a camera driver and higher-level vision processing."
url='https://wiki.ros.org/image_pipeline'

pkgname='ros-noetic-image-pipeline'
pkgver='1.17.0'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

ros_makedepends=(
	ros-noetic-catkin
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
	ros-noetic-image-rotate
	ros-noetic-stereo-image-proc
	ros-noetic-depth-image-proc
	ros-noetic-image-view
	ros-noetic-image-proc
	ros-noetic-image-publisher
	ros-noetic-camera-calibration
)

depends=(
	${ros_depends[@]}
)

_dir="image_pipeline-${pkgver}/image_pipeline"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-perception/image_pipeline/archive/${pkgver}.tar.gz")
sha256sums=('2439fbd1165b128da9d7663ebc1a7fee0f97b8f05427a3d2f7a82b782dcbc090')

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
