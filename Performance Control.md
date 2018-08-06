# Performance Control of TX1

## Background
Once JetPack installation is done, you will soon notice problems of day-to-day normal computer usage,  
especially like browsing the internet is very difficult. 

For example, the video was playing erratically when I tried the tutorial of migrating OS to SD card on YouTube -  
skips frames and even freezes not only the browser but also the TX1 board itself.

After a few search I found this is due to the nature of L4T OS.  
In which, you have to manually adjust the hardware clock.

## Reference
https://elinux.org/Jetson/TX1_Controlling_Performance  
https://elinux.org/Jetson/Performance  
https://wiki.archlinux.org/index.php/CPU_frequency_scaling  
https://androidforums.com/threads/android-cpu-governors-explained.513426/  

## For TX1 with JetPack 3.2
Most of code provided in above reference link are outdated because directory structure varies by L4T OS version.  
For example, `/sys/kernel/debug/clock` has changed to `/sys/kernel/debug/clk` in L4T 28.2.  

```
	# Fan Control #
# sudo chown -R nvidia:nvidia /sys/kernel/debug/
echo 200 > /sys/kernel/debug/tegra_fan/target_pwm  

	# Read Temperature #
cat /sys/devices/virtual/thermal/thermal_zone*/type
cat /sys/devices/virtual/thermal/thermal_zone*/temp

	# CPU Control #
# sudo chown -R nvidia:nvidia /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
echo "Online CPUs: `cat /sys/devices/system/cpu/online`"
for i in 0 1 2 3 ; do
	echo 1 > /sys/devices/system/cpu/cpu${i}/online
done
echo interactive > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

	# GPU Control #
cat /sys/kernel/debug/clk/gbus/max > /sys/kernel/debug/clk/override.gbus/clk_rate
echo 1 > /sys/kernel/debug/clk/override.gbus/state
echo "GPU: `cat /sys/kernel/debug/clk/gbus/clk_rate`"
  
```

## Balance Between Power, Thermal and Performance
https://elinux.org/Jetson/Jetson_TK1_Power
