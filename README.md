export wrfdir=/home/wrf/WRF/WPS
export wrfdir=/home/wrf/WRF/WRF

rm wrfbdy* wrfinput* wrfout*
ln -sf $wrfdir/run/*.TBL .
ln -sf $wrfdir/run/ozone* .
ln -sf $wrfdir/run/RRTMG* .
ln -sf $wrfdir/run/CAM* .
ln -sf $wrfdir/run/*.exe .
ln -sf $wpsdir/*.exe .
