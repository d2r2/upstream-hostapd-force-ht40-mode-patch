Patch for upstream hostapd to force 40MHz operation
===================================================

This patch is completely based on beautiful hostapd fork: https://github.com/ivkos/hostap-force-ht40.

Purpose of this project - to get hostapd installation which work good in modern urban conditions,
where radio air is filled with neighboring Wi-Fi points. Without this modification hostapd service regularly fallback to 20MHz mode, reporting that there are overlapping BSSes exist around.

Aim of this project - to have minimal patch for upstream hostapd release, without necessity to keep the whole hostapd branch in sync with upstream sources.

Disclamer 1
-----------
Remember that this change is in violation of IEEE Std 802.11-2012, 10.15.3.2 and is entirely on your conscience.

Disclamer 2
-----------
I'm not recommended to use hostapd with wifi hardware adapters based on Realtek chipsets. My personal experience demonstrate - Realtek had bad support of nl80211 netlink interface, and, as a result, hostapd behavior looks buggy with Realtek hardware. Opposite - and this is again from my personal experience - Ralink network devices work stably and reliably with hostapd.


Compilation and installation
----------------------------

* Download and unzip current stable hostapd sources: https://w1.fi/hostapd/ (Latest release section).
* Copy patch file `upstream-hostapd-force-ht40-mode.patch` from here to hostapd source root folder (where hostapd, src folders located).
* Run `patch -p0 < upstream-hostapd-force-ht40-mode.patch` to apply patch.
* Execute hostapd compilation with `make` with futher installation with `make install`.
* Add `force_ht40=1` option to hostapd.conf file to force 40MHz mode.
* Start hostapd service.

>Note 1: Do not forget to copy deconfig to .config and uncomment `#CONFIG_IEEE80211N=y`, before hostapd compilation.
>Note 2: You can additionally monitor how your hostapd service work via such Android application as "WiFi Analyzer".

Tested with equipment
---------------------

* Orance PI Zero Plus with external WiFi adapter COMFAST CF-WU7300ND (Ralink RT3072 chipset) 2.4Ghz.

Contact
-------

Please use [Github issue tracker](https://github.com/d2r2/upstream-hostapd-force-ht40-mode-patch/issues) for filing bugs or feature requests.


License
-------

Licensed under BSD License.
