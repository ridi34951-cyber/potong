# Camera — GyroLock V28.6 (anchor-lock tuning)

This revision tunes the offline gyro correction to resist gentle left/right aiming and small phone tilts instead of letting the stabilized scene drift with them. The camera path is compared with a 4.0-second centered reference trajectory, correction gain is 0.94, correction limits are slightly wider, correction smoothing is 0.22 seconds, and the render crop is increased to 1.16× to provide more stabilization margin.

The goal is to keep a scene anchor visually steady during small and medium movements. A finite crop cannot hold every scene point forever during a long intentional pan; once the correction reaches its safe limit, some drift or edge distortion is unavoidable. Mirrored edge sampling remains enabled. This revision keeps Android 13+ (`minSdk 33`), the Vulkan renderer, 240 trajectory points, 30 FPS output timeline, and audio remux path.

This is a source-level tuning, not a verified performance claim: the APK has not been built or tested on-device in this environment. Compare the original and stabilized output with a fixed subject while making slow small pans and tilts. If it moves in the same direction as the camera or counter-moves visibly, the next step is to calibrate the gyro-to-camera axis/sign mapping using a short test clip; smoothing alone cannot correct a wrong axis mapping.
