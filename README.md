# .-.
What I tried on Apple Silicon Macs.

### Running the latest x86_64 wine on Apple Silicon macs with 3D acceleration.

#### 2022/04

* Build the wine source: `wine64` on Rosetta 2 only available.
  - aarch32 is not implemented on Apple Silicon.
  - Apple dropped support for 32-bit applications since macOS Catalina.
  - It could not run PE32(most of the installers, programs) windows executables since there is no WoW64 (Windows 32-bit on Windows 64-bit) support.
<br>

* Use Crossover: worked via `wine32on64` on Rosetta 2, but It's LAME.
  - Currently, The latest Crossover is based on wine 6.0 sources.
<br>

* [Port Crossover Wine to regular latest wine](https://github.com/CalicoCheese/wine-cx-port).
  - I succeeded in merging nearly 4000 files, but many errors occurred while building. (That was a reckless challenge ;) )
  - Need to check out the wine32on64 tricks more.
<br>

* Running arm64 Linux machines on `VMware Fusion Tech Preview` and execute `wine`/`wine64` via qemu-userspace emulations.
  - It could not create a wine prefix. (crashed `wine`, cannot be executed anymore.)
  - VirtualGL software accelerations. (VGL Transport with X11 Forwarding)
<br>

* Running arm64 Linux machines on `VMware Fusion Tech Preview` and execute `wine`/`wine64` via `box86`/`box64`.
  - `box86` could not be executed since there is no aarch32 support.
  - `wine`: there is no `wine` & WoW64 supports because `box86` is missing.
  `wine64`: runs perfectly via `box64` (not usually for games).
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
   - Extremely slow. (because there is no `hypervisor.framework` acceleration support on x86_64 virtual machines.)
   - `wine`/`wine64` crashed. (The winedbg opens and it cannot create a wine prefix.)
   - VirtualGL software accelerations. (VGL Transport with X11 Forwarding)
<br>

* Running arm64 Linux machines on `qemu` [**with GPU acceleration**](https://gist.github.com/akihikodaki/87df4149e7ca87f18dc56807ec5a1bc5) and execute `wine`/`wine64`.
   - ~~I'm using M1 Pro, [there is have an issue](https://gist.github.com/akihikodaki/87df4149e7ca87f18dc56807ec5a1bc5?permalink_comment_id=4064827#gistcomment-4064827), so I used [patched akihikodaki's qemu](https://github.com/hurrhnn/qemu-hvf-patch/commit/bc0d5c2628c930caba57a7c191cac3e74ee49018)~~ -> resolved from upstream.
   - As far as I know, there is no way to run `wine` normally with x86_64 emulation I think.
   - Hardware 3D accelerations using QEMU virgl.
<br>

* Running arm64 Windows machines (Windows 11 Insider Preview) on `UTM(QEMU)`.
  - x86, x64 emulation is available in Windows 11.
  - x86, x64 emulation is even slower than macOS Crossover.
  - General 2D accelerations.
<br>

#### 2022/12

* Use Crossover: worked via `wine32on64` on Rosetta 2, but It's still unstable.
  - Currently, The latest Crossover is based on wine 7.7 sources.
<br>

* Running arm64 Linux machines on [`VMware Fusion Tech Preview 22H2`](https://blogs.vmware.com/teamfusion/2022/07/just-released-vmware-fusion-22h2-tech-preview.html) and execute `wine`/`wine64` via `box86`/`box64`.
  - It requires the **super latest** linux system (I usually use Fedora Rawhide(38) for this).
  - `box86` could not be executed since there is no aarch32 support.
  - `wine`: there is no `wine` & WoW64 support because `box86` is missing.
  - `wine64`: runs perfectly via `box64` (not usually for games).
  -  Hardware 3D accelerations using vmwgfx.
<br>

* Running arm64 Linux machines on [`VMware Fusion Tech Preview 22H2`](https://blogs.vmware.com/teamfusion/2022/07/just-released-vmware-fusion-22h2-tech-preview.html) and execute `wine`/`wine64` via `FEX-emu`.
  - Not tested, I'll do this If I have time left.
<br>

* Running arm64 Linux machines on `utm(qemu)` and execute `wine`/`wine64` via [`Rosetta 2 Passthrough`](https://developer.apple.com/documentation/virtualization/running_intel_binaries_in_linux_vms_with_rosetta).
  - `wine`: there is no `wine` & WoW64 support since there is no x86(i686) support on Rosetta 2.
  - `wine64`: not tested.
