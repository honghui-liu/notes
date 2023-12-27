---
layout: post
title: "Useful material for projects"
---

This page is used to record the useful links, commands and softwares that I found can be very helpful for doing projects.

## Links

### Tools

* The Galactic nH calculator: [engage!](https://www.swift.ac.uk/analysis/nhtot/index.php)
* RA DEC flexible converter: [click me](http://www.astrouw.edu.pl/~jskowron/ra-dec/)
* Online tool for coordinate transformation: [Ned site](https://ned.ipac.caltech.edu/forms/calculator.html)
* MJD converter: [here it is](http://www.csgnetwork.com/julianmodifdateconv.html)
* Date/time conversion: [xTime](https://heasarc.gsfc.nasa.gov/cgi-bin/Tools/xTime/xTime.pl)
* Plotting with PLT: [here](https://heasarc.gsfc.nasa.gov/docs/xte/recipes/plotting.html), [Label](https://heasarc.gsfc.nasa.gov/ftools/others/qdp/node136.html`)
* The ftool ftgrouppha: [click](https://heasarc.gsfc.nasa.gov/lheasoft/ftools/headas/ftgrouppha.html)
* Xselect: [Introduction](https://www.swift.ac.uk/analysis/xrt/xselect.php), [Guide](https://heasarc.gsfc.nasa.gov/ftools/xselect/node1.html)
* Spearman's Critical Correlation Calculator: [1](https://mathcracker.com/spearmans-critical-correlation-calculator#results), [Calculator](https://geographyfieldwork.com/SpearmansRankCalculator.html#Strength-of-Correlation), [Pearson and Spearman](https://www.jianshu.com/p/93a3861e8edc), [python module](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.spearmanr.html).
* A Mission Count Rate Simulator: [WebPIMMS](https://heasarc.gsfc.nasa.gov/cgi-bin/Tools/w3pimms/w3pimms.pl).
* Online pipeline for processing Swift XRT data: [link](https://www.swift.ac.uk/user_objects/)
* The interactive analysis interface for Swift: [link](https://www.ssdc.asi.it/mmia/index.php?mission=swiftmastr)

### Data base

* Atomic database for astrophysicists: [ATOMDB](http://www.atomdb.org/)
* NASA/IPAC Extragalactic Database (NED): https://ned.ipac.caltech.edu/
* SIMBAD: http://simbad.u-strasbg.fr/simbad/sim-fid

### Catalog

* Swift Hard X-ray Survey: [Let's go](https://swift.gsfc.nasa.gov/results/bs105mon/)
* Swift/BAT Hard X-ray Transient Monitor: [link](https://swift.gsfc.nasa.gov/results/transients/)
* The Swift-XRT Point Source catalog: [2SXPS](https://www.swift.ac.uk/2SXPS/)
* The black hole XRB monitor: [link](http://integral.esac.esa.int/blackholemonitor/black-hole-monitor.php)

### Website

* Homepage of: [Cosimo Bambi](http://www.physics.fudan.edu.cn/tps/people/bambi/Site/Home.html)
* The Cambridge group: [Here](https://www-xray.ast.cam.ac.uk/)
* Heasarc FTP: [go](https://heasarc.gsfc.nasa.gov/FTP/)
* Search for observations: [browse](https://heasarc.gsfc.nasa.gov/cgi-bin/W3Browse/w3browse.pl)

### Workshop

* X-ray spectral fitting methods workshop: [here](https://www.mpe.mpg.de/resources/HE/Buchner/xrayworkshop/?fbclid=IwAR3aKISdmmASKO-IeX3skdzgFREszKa16WFbACG_tj-FQnHqeY0GYkFHyGs)
* The 2020 AtomDB workshop: [link](http://www.atomdb.org/Meetings/2020/)
* KouShare: https://www.koushare.com/video/videosearch

### Software

* The CLOUDY homepage: [CLOUDY](https://www.nublado.org/)
* XSTAR: https://heasarc.gsfc.nasa.gov/xstar/xstar.html
* Bayesian X-ray Analysis: [BXA](https://johannesbuchner.github.io/BXA/?fbclid=IwAR0Hf-m33oBYmiL_dMBqN0UB2ZWQdvKLxxDxJk79q4fRGHPSTR47P0NJpow)
* Code for HXMT data treatment (by Prof. Long Ji): http://code.ihep.ac.cn/jldirac/insight-hxmt-code-collection/-/tree/master
* Stingray, a very useful python package for X-ray timing analysis and treatment of lightcurve data.
  * Website: https://docs.stingray.science/en/v1.1.2.2/
  * Github: https://github.com/StingraySoftware/stingray

## Tutorials

- How to install calibration: [click](https://heasarc.gsfc.nasa.gov/docs/heasarc/caldb/caldb_install.html)

### Others

* X-ray transition energies: [go](https://www.nist.gov/pml/x-ray-transition-energies-database)
* The chi-square table: [chi](http://www.reid.ai/2012/09/chi-squared-distribution-table-with.html)
* Uncertainty transformation: [click](https://www.cnblogs.com/heaventian/archive/2012/11/24/2786241.html), [theory](https://phas.ubc.ca/~oser/p509/Lec_10.pdf)

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

* To use [optimal binning](https://arxiv.org/abs/1601.05309) strategy with ftool `ftgrouppha`([usage](https://heasarc.gsfc.nasa.gov/lheasoft/ftools/headas/ftgrouppha.html))

```
ftgrouppha infile=MAXIJ1535_LE_chkey.pha backfile=MAXIJ1535_LE_bkg.pha outfile=MAXIJ1535_LE_opt.pha grouptype=opt respfile=MAXIJ1535_LE.rsp clobber=yes
```
