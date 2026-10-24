# Patched mpv-android

`app/libs/mpv-android-1.0.0-dolby-vision.aar` is built from
[`marlboro-advance/mpv-android`](https://github.com/marlboro-advance/mpv-android)
commit `0a762048a4f3a96e0102a8a0609a0505d6b57f7f` with FFmpeg `n9.0` commit
`d32b387f2b0a484599d4587d651891f0c63c4238` and
`patches/ffmpeg-mediacodec-dolby-vision-profile5.patch`.

The patch makes FFmpeg's MediaCodec decoder request Android's
`video/dolby-vision` MIME for HEVC Dolby Vision Profile 5 streams. Other HEVC
and Dolby Vision profiles retain the upstream `video/hevc` path.

## Rebuild

On Linux with an Android SDK in `ANDROID_HOME`:

```sh
git clone https://github.com/marlboro-advance/mpv-android.git
cd mpv-android
git checkout 0a762048a4f3a96e0102a8a0609a0505d6b57f7f
./buildscripts/ci.sh install
git -C buildscripts/deps/ffmpeg apply \
  /path/to/ffmpeg-mediacodec-dolby-vision-profile5.patch
./buildscripts/buildall.sh -n --clean ffmpeg --arch armv7l
./buildscripts/buildall.sh -n --clean ffmpeg --arch arm64
./buildscripts/ci.sh build
```

Copy `app/build/outputs/aar/app-release.aar` to
`app/libs/mpv-android-1.0.0-dolby-vision.aar` in this repository. The checked-in
AAR has SHA-256
`c1649be9d541e6905c742c50c0b5fb5dab0f7ed92b9946747722565b5c732825`.
