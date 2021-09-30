A (practical) tutorial for very (very) beginners in [Bambi's Gravity group of Fudan](http://www.physics.fudan.edu.cn/tps/people/bambi/Site/Home.html).

# How to begin a project

[toc]

## Softwares

Usually it is convient to work remotely on the cluster since data analysis can be demanding for computation power. So it's better to install necessary applications for connecting to the cluster.

- For Windows user: There are many options and tons of tutorials online. For instance:
	- The Windows subsystem for linux (WSL) + Xming (for plotting)
	- Putty + Xming
	- Xmanager
	- Cygwin
- For Mac user: Use `ssh` in the Terminal to connect the cluster, but you still need to install `Xquartz` for plotting in XSPEC.
- For linux user: You know what to do and nothing is needed to be installed.

To login to the cluster, just type `ssh -p 22 -XY [username]@[ip]` in the terminal, where [username] is your account on the cluster and [ip] is the ip address.

## Download data

Let's say you have already known what project to do and had in mind which source to analyze. Then the first thing is to download the data.

The data we need can usually be downloaded from Heasarc. If you already know which source (or even which observation) to study, you can visit [this website](https://heasarc.gsfc.nasa.gov/cgi-bin/W3Browse/w3browse.pl) to look for the data. Just type in the source name (e.g. Cyg X-1), choose the satellite and `Start Search`.

Then you should see the `Query Results`, you can just select the rows you want to download and click `Retrieve Data Products for selected rows` in the bottom of the result page. Click `Creat Download Script` and then you can see the script in bold like this:

```
wget -q -nH --no-check-certificate --cut-dirs=6 -r -l0 -c -N -np -R 'index*' -erobots=off --retr-symlinks https://heasarc.gsfc.nasa.gov/FTP/nustar/data/obs/05/9//90501314002/
```

Copy the script and run it in the terminal until the downloading finishes.

## Reduce data

The data downloaded following the last section is 'raw data'. Generally, it has to be reduced for any scientific purpose. The data reduction procedure is different for different instruments. Here is a list for data reduction manuals of several X-ray missions:

- XMM-Newton: [My blog](https://honghui-liu.github.io/notes/2020/02/27/XMM-data-reduction.html) and references there in:)
- Suzaku: [My reduction script](https://github.com/honghui-liu/suzaku_reduction).
- NuSTAR: The [NuSTARDAS guide](https://heasarc.gsfc.nasa.gov/docs/nustar/analysis/nustar_swguide.pdf) and a [quick guide](https://heasarc.gsfc.nasa.gov/docs/nustar/analysis/nustar_quickstart_guide.pdf)

## Relxill_nk model

`Relxill_nk` is a non-Kerr version of [relxill](http://www.sternwarte.uni-erlangen.de/~dauser/research/relxill/) model. It describes the reflected spectrum from an geometrically thin and optically thick accretion disk. The incident spectrum is often assumed as a power-law with high energy cutoff.

There are several parameters in the model. Before explaining the meaning of these models, let us think a bit this question: What things are necessary to be known before we can calculate the reflected spectrum from an accretion disk?

First, we have to know the incident spectrum, without which there will be no reflection. In `relxill_nk`, we usually assume the spectrum of the incident radiation to be a [powerlaw with high energy cutoff](https://heasarc.gsfc.nasa.gov/xanadu/xspec/manual/node162.html). There are three parameters to describe a `power-law` component:

- `PhotonIndex` (`gamma`): The index of a power-law function.
- `Ecut`: The high enegry cutoff.
- `Norm`: Normalization.

It's also necessary to know how the incident radiation is distributed on the disk. Or let's say, the intensity of the incident radiation as a function of disk radius (the **emissivity profile**). In principle, this distribution can be self-consistently calculated if the disk-corona geometry is known (e.g. if the corona is a point source above a $a_{*}=0.9$ black hole at height $h$). Here the **corona** is the X-ray source illuminating the accretion disk (the source that emits the `power-law` radiation to the accretion disk). In practice, a phenomenological emissivity profile in the form of broken power-law is commenly used to fit the reflection spectra. Please distinguish the **power-law emission from the corona** and the **power-law emissivity profile**! **Power-law** is just a kind of function that has format: $f(x)=ax^{-k}$. 

Then, the **disk geometry and its physical properties** (inclination, inner and outer radius, density, temperature, ionization, element abundances) are also key ingredients. The inclination of the inner disk, together with the inner radius, will affect the strength of Doppler shifting on the photons emitted from the disk. The inner radius of the disk is also important for calculating the gravitational redshift of the photons.

The last component is the **spacetime**. The photons emitted in the vicinity of black holes will inevitably affected by the strong gravity field. This must be taken into account when modeling the reflected spectra from the inner accretion disk. It is also for this reason that the relativistic reflection spectrum can be used to probe the strong gravity field (e.g., measure the black hole spin) and to test gravity theory. For a Kerr black hole, the spacetime metric can be fully described by three parameters: black hole mass ($M$), black hole spin ($a_*$) and electric charge ($Q$). The influence of electric charge on the reflection spectrum is negligible. The black hole mass is not needed in the calculation of reflection spectrum when measuring length scale in gravitational radius ($r_g=GM/c^2$). In the end, there is only one parameter, the black hole spin ($a_*$), left in the reflection model. 

## Some references

- Reviews on black hole spin measurement with relativistic reflection features: [Bambi et al., 2021](https://ui.adsabs.harvard.edu/abs/2021SSRv..217...65B/abstract), [Reynolds et al., (2014)](https://ui.adsabs.harvard.edu/abs/2014SSRv..183..277R/abstract). In Bambi et al., (2021), there is good description of different relativistic reflection models commonly used in this field and discussion about systematic uncertainties due to simplification in modeling, instrumental uncertainty and the lack of knowledge of the system.
- About testing general relativity using X-ray reflection spectroscopy: 
  - Justification of the methodology: [Bambi et al., 2017a](https://ui.adsabs.harvard.edu/abs/2017ApJ...842...76B/abstract), [Bambi et al., 2017b](https://ui.adsabs.harvard.edu/abs/2017RvMP...89b5001B/abstract).
  - Practical implementation: [Tripathi et al., 2021a](https://ui.adsabs.harvard.edu/abs/2021ApJ...913...79T/abstract) (the NuSTAR survey on BHXRBs), [Zhang et al., 2021](https://ui.adsabs.harvard.edu/abs/2021PhRvD.103b4055Z/abstract) (Cygnus X-1), [Tripathi et al., 2021b](https://ui.adsabs.harvard.edu/abs/2021ApJ...907...31T/abstract) (GX 339-4), [Liu et al., 2020](https://ui.adsabs.harvard.edu/abs/2020ApJ...896..160L/abstract) (Fairall 9), [Zhang et al., 2019](https://ui.adsabs.harvard.edu/abs/2019ApJ...884..147Z/abstract) (GRS 1915+105), [Liu et al., 2019](https://ui.adsabs.harvard.edu/abs/2019PhRvD..99l3007L/abstract) (Cygnus X-1), [Tripathi et al., 2019](https://ui.adsabs.harvard.edu/abs/2019ApJ...875...56T/abstract) (MCG 06-30-15), [Tripathi et al, 2019b](https://ui.adsabs.harvard.edu/abs/2019ApJ...874..135T/abstract) (Suzaku survey on bare AGNs). See Table 5 of [Zhang et al., 2021](https://arxiv.org/pdf/2106.03086.pdf) for a more complete collection.
- **Must-read** before using XSPEC for data analysis
  - The fourth chapter of [XSPEC manual](https://heasarc.gsfc.nasa.gov/xanadu/xspec/manual/XspecManual.html): [Walks through XSPEC](https://heasarc.gsfc.nasa.gov/xanadu/xspec/manual/node35.html) 
  - A useful [XSPEC tutorial](http://labx.iasfbo.inaf.it/2014/resources/xspec_tutorial2014.pdf).

## Some exercise

It is better to understand the questions (at least qualitatively) below if analyzing real data.

### About spectral files

- Copy the simulated files to your dir on cluster 1

  ```bash
  $>mkdir exercise
  $>cd exercise
  $>cp /home/honghui/files/exercise/* ./
  $>ls
  ```

- The source ("simulation_fpmb.pha") and background (simulation_fpmb_bkg.pha) spectra.

  - What is stored in the source and background spectra files? (A: channels, counts, exposure time)

- The response files

  - What is in rmf file? (Channel -> energy)
  - What is in arf file? (effective area)

### About fitting in XSPEC

- Why is it necessary to group data if chi-squared statistic is used? (Poisson -> gaussian)
- How is chi-square calculated? (There is answer the XSEPC manual)
- How to import two spectra to XSPEC? 
  - `data 1:1 spec1.pha 2:2 spec2.pha`
  - Figure out the meaning of these numbers (1:1) in the command above.
  - How to account for the cross normalization between different instruments?
- How to get the uncertainties (errorbars, constraints) of certain parameters? (`error` command in XSPEC)
- What is degeneracy of parameters and how to estimate the degeneracy?
  - `steppar` command in XSPEC.

### About the iron line

```bash
$>xspec
XSPEC>data simulation_fpmb_grp100.pha
XSPEC>ignore **-3.0 79.0-**
XSPEC>query yes
XSPEC>model tbabs*cutoffpl
XSPEC>fit
XSPEC>cpd /xs
XSPEC>setplot energy
XSPEC>plot ra
```

- Do you see the iron line and Compton hump?
- Can you fit the spectra with `relxill` model and recover the input parameters for simulation? (nH=0.6, a=0.998, incl=30.0, index1=index2=3, gamma=2.0, logxi=3.0, Afe=1.0).
- Can you report the uncertainties for each parameter?

## A few other things

### Some principles of making plots

- The fontsize of the annotations and labels should at least be larger than the caption in the paper.



Last edited on 2021/09/27 by [Liu Honghui](https://honghui-liu.github.io/).
