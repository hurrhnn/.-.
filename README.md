# .-.
What I tried on Apple Silicon Macs.

### Running the latest x86_64 wine on Apple Silicon macs with 3D acceleration.

* Build the wine source: `wine64` on Rosetta 2 only available.
  - aarch32 is not implemented on Apple Silicon.
  - Apple dropped support for 32-bit applications since macOS Catalina.
  - It cannot run PE32(most of the installers, programs) windows executables since there is no WOW64 support.
<br>

* Use Crossover: worked via `wine32on64` on Rosetta 2, but It's LAME.
  - Currently, The latest Crossover is based on wine 6.0 sources. It's not horny.
<br>

* [Port Crossover Wine to regular latest wine](https://github.com/CalicoCheese/wine-cx-port).
  - I succeeded in merging nearly 4000 files, but many errors occurred while building. (That was a reckless challenge ;) )
  - need to check out the wine32on64 tricks more.
<br>

* Running arm64 Linux machines on `VMware Fusion Tech Preview` and execute `wine`/`wine64` via qemu-userspace emulations.
  - It cannot create a wine prefix. (crashed `wine`, cannot be executed anymore.)
  - VirtualGL software accelerations. (VGL Transport with X11 Forwarding)
<br>

* Running arm64 Linux machines on `VMware Fusion Tech Preview` and execute `wine`/`wine64` via `box86`/`box64`.
  - `box86` cannot be executed since there is no aarch32 support.
  - `wine`: there is no `wine` & WOW64 support because `box86` is missing.
  - `wine64`: runs perfectly via `box64`.
  - VirtualGL software accelerations. (VGL Transport with X11 Forwarding)
<br>

* Running arm64 Linux machines on `VMware Fusion Tech Preview` and execute `wine`/`wine64` via `FEX-emu`.
  - `wine`: wine 6.0 version or higher be crashed.
  - `wine64`: Segmentation fault.
  - VirtualGL software accelerations. (VGL Transport with X11 Forwarding)
<br>

* Running arm64 Linux machines on `UTM(qemu)` and execute `wine`/`wine64`.
   - Same as above `VMware Fusion Tech Preview`.
<br>

* Running **x86_64** Linux machines on `UTM(qemu)` and execute `wine`/`wine64`.
   - Extremely slow. (because there is no `hypervisor.framework` acceleration support on x86_64 machines.)
   - `wine`/`wine64` crashed. (The winedbg opens and it cannot create a wine prefix.)
   - VirtualGL software accelerations. (VGL Transport with X11 Forwarding)
<br>

* Running arm64 Linux machines on `qemu` [**with GPU acceleration**](https://gist.github.com/akihikodaki/87df4149e7ca87f18dc56807ec5a1bc5) and execute `wine`/`wine64`.
   - I'm using M1 Pro, [there is have an issue](https://gist.github.com/akihikodaki/87df4149e7ca87f18dc56807ec5a1bc5?permalink_comment_id=4064827#gistcomment-4064827), so I used [patched akihikodaki's qemu](https://github.com/hurrhnn/qemu-m1-patch/commit/8be614e0bb870121ddfbe2620b3e2871e03bb817).
   - As far as I know, there is no way to run `wine` normally with x86_64 emulation I think.
   - Hardware 3D accelerations. (Linux guest OS only.)
<br>

* Running arm64 Windows machines (Windows 11 Insider Preview) on `UTM(QEMU)`.
  - x86, x64 emulation is available in Windows 11.
  - x86, x64 emulation is even slower than macOS Crossover.
  - General 2D accelerations.
  - ![image](https://user-images.githubusercontent.com/40728528/161310330-8e6ae9e9-bdf6-480a-9020-25efdf5b861b.png)
  - ![image](https://user-images.githubusercontent.com/40728528/161308478-b5149675-9404-4848-8b81-838d7b3195d0.png)
<br>
