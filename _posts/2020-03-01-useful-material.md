---
layout: post
title: "Useful material for projects"
---

*This page is used to record the useful links, commands and references that I found can be very helpful for doing projects.*

## Links

### Tools

* Atomic database for astrophysicists: [ATOMDB](http://www.atomdb.org/)
* The Galactic nH calculator: [engage!](https://www.swift.ac.uk/analysis/nhtot/index.php)
* RA DEC flexible converter: [click me](http://www.astrouw.edu.pl/~jskowron/ra-dec/)
* MJD converter: [here it is](http://www.csgnetwork.com/julianmodifdateconv.html)
* Plotting with PLT: [here](https://heasarc.gsfc.nasa.gov/docs/xte/recipes/plotting.html)
* The ftool ftgrouppha: [click](https://heasarc.gsfc.nasa.gov/lheasoft/ftools/headas/ftgrouppha.html)
* Xselect: [Introduction](https://www.swift.ac.uk/analysis/xrt/xselect.php), [Guide](https://heasarc.gsfc.nasa.gov/ftools/xselect/node1.html)

### Catalog

* Swift Hard X-ray Survey: [Let's go](https://swift.gsfc.nasa.gov/results/bs105mon/)
* The Swift-XRT Point Source catalog: [2SXPS](https://www.swift.ac.uk/2SXPS/)

### Website

* Homepage of: [Cosimo Bambi](http://www.physics.fudan.edu.cn/tps/people/bambi/Site/Home.html)
* The Cambridge group: [Here](https://www-xray.ast.cam.ac.uk/)
* Heasarc FTP: [go](https://heasarc.gsfc.nasa.gov/FTP/)

### Workshop

* X-ray spectral fitting methods workshop: [here](https://www.mpe.mpg.de/resources/HE/Buchner/xrayworkshop/?fbclid=IwAR3aKISdmmASKO-IeX3skdzgFREszKa16WFbACG_tj-FQnHqeY0GYkFHyGs)

### Software

* The CLOUDY homepage: [CLOUDY](https://www.nublado.org/)

### Others

* X-ray transition energies: [go](https://www.nist.gov/pml/x-ray-transition-energies-database)
* The chi-square table: [chi](http://www.reid.ai/2012/09/chi-squared-distribution-table-with.html)
* Uncertainty transformation: [click](https://www.cnblogs.com/heaventian/archive/2012/11/24/2786241.html)

## References

## Commands

* To visualize the light curve

```
lcurve nser=1 cfile1=rate.fits window="-" dtnb=50 nbint=3000 outfile="lc" plot=yes plotdev="/xs"
```

* To group data with <code>grppha</code>

```
grppha source_spectrum.fits pn_25.grp comm= "chkey RESPFILE pn.rmf & chkey ANCRFILE pn.arf & chkey BACKFILE back_spectrum.fits & group min 25 & exit"
```

* To download data with FTP from nasa's archive

```
wget -q -nH --no-check-certificate --cut-dirs=3 -r -l0 -c -N -np -R 'index*' -erobots=off --retr-symlinks https://heasarc.gsfc.nasa.gov/FTP/caldb/data/suzaku/
```

* To use [optimal binning](https://arxiv.org/abs/1601.05309) strategy with ftool <code>ftgrouppha</code>

```
ftgrouppha infile=MAXIJ1535_LE_chkey.pha backfile=MAXIJ1535_LE_bkg.pha outfile=MAXIJ1535_LE_opt.pha grouptype=opt respfile=MAXIJ1535_LE.rsp clobber=yes
```