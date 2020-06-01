HDD/SSD Reliability Test
========================

This is a project to estimate reliability of HDD/SSD drives by
the analysis of SMART data collected by BSD users at https://bsd-hardware.info. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe/blob/master/INSTALL.BSD.md) tool:

    hw-probe -all -upload

Total drives: 321.

Contents
--------

1. [ About          ](#about)
2. [ HDD by Model   ](#hdd-by-model)
3. [ HDD by Family  ](#hdd-by-family)
4. [ HDD by Vendor  ](#hdd-by-vendor)
5. [ SSD by Model   ](#ssd-by-model)
6. [ SSD by Family  ](#ssd-by-family)
7. [ SSD by Vendor  ](#ssd-by-vendor)
8. [ NVMe by Model  ](#nvme-by-model)
9. [ NVMe by Vendor ](#nvme-by-vendor)

About
-----

The structure of the reports directory is the following:

    {KIND OF DRIVE}/{VENDOR}/{MODEL PREFIX}/{MODEL}/{DRIVE ID}

    ( e.g. HDD/Seagate/ST1000/ST1000LM035-1RK172/3F1554E2F97E )

Based on SMART data we determine most reliable drive models and vendors by the
following formula:

    MTBF = MAX( Power_On_Hours / ( 1 + Number_Of_Important_Errors ) ) / ( 365*24 )

    ( i.e. MTBF = "Years before/between errors" )

Number_Of_Important_Errors — number of important errors that can indicate a drive failure:

* Current_Pending_Sector
* ECC_Uncorr_Error_Count
* End-to-End_Error
* Offline_Uncorrectable
* Reallocated_Event_Count
* Reallocated_Sector_Ct
* Reported_Uncorrect
* Soft_Read_Error_Rate
* Spin_Retry_Count
* Total_Pending_Sectors
* Unc_Soft_Read_Err_Rate

One can estimate reliability of a hard drive (i.e. probability that the unit will work
for some time T without failure) by:

    Reliability(T) = exp(-T/MTBF)

The list of important SMART attributes is taken from recent studies of Google [1],
Backblaze [2] and Acronis [3]. If an attribute exceeds the value of 1000 then it's
counted as '1000 + log10(X - 999)'.

The list of tracked attributes and MTBF calculation method can be discussed. Please
suggest your ideas in "issues".

You can perform your own analysis of collected reports if needed.

* [1] Google, "Failure Trends in a Large Disk Drive Population" (https://research.google.com/archive/disk_failures.pdf)
* [2] Backblaze, "Hard Drive SMART Stats" (https://www.backblaze.com/blog/hard-drive-smart-stats/)
* [3] Acronis, "Acronis Drive Monitor: Disk Health Calculation" (https://kb.acronis.com/content/9264)

HDD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

See complete list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Seagate   | ST3120023A         | 120 GB | 1       | 5214  | 0     | 14.29  |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 3       | 4223  | 0     | 11.57  |
| WDC       | WD1600JD-00GBB0    | 160 GB | 4       | 5313  | 4     | 11.14  |
| Seagate   | ST3500630NS        | 500 GB | 1       | 4005  | 0     | 10.97  |
| Hitachi   | HDS725050KLA360    | 500 GB | 1       | 3763  | 0     | 10.31  |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 4       | 3039  | 0     | 8.33   |
| Hitachi   | HDT725025VLA380    | 250 GB | 1       | 2680  | 0     | 7.34   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 2       | 2469  | 0     | 6.77   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 1       | 2461  | 0     | 6.74   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 1       | 2398  | 0     | 6.57   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 1       | 2374  | 0     | 6.51   |
| Seagate   | ST3160318AS        | 160 GB | 1       | 2290  | 0     | 6.27   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 1       | 2233  | 0     | 6.12   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 1       | 2187  | 0     | 5.99   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 3       | 2169  | 0     | 5.94   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 2       | 2071  | 0     | 5.68   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 1       | 2024  | 0     | 5.55   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 2       | 2015  | 0     | 5.52   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 2       | 2009  | 0     | 5.51   |
| Toshiba   | DT01ACA200         | 2 TB   | 3       | 1992  | 0     | 5.46   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 3       | 1988  | 0     | 5.45   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 2       | 1933  | 0     | 5.30   |
| Seagate   | ST3320620A         | 320 GB | 1       | 1913  | 0     | 5.24   |
| Seagate   | ST3500413AS        | 500 GB | 2       | 1885  | 0     | 5.17   |
| Samsung   | HD501LJ            | 500 GB | 4       | 3871  | 3     | 5.15   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 1       | 1870  | 0     | 5.12   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 1       | 1848  | 0     | 5.06   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 2       | 1786  | 0     | 4.90   |
| Seagate   | ST3320620AS        | 320 GB | 1       | 1737  | 0     | 4.76   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 1       | 1673  | 0     | 4.58   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 2       | 1670  | 0     | 4.58   |
| Seagate   | ST3250318AS        | 250 GB | 1       | 1636  | 0     | 4.48   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 1       | 1633  | 0     | 4.48   |
| Seagate   | ST91000640NS       | 1 TB   | 1       | 1630  | 0     | 4.47   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 1       | 1591  | 0     | 4.36   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 3       | 3153  | 4     | 4.05   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 2       | 1408  | 0     | 3.86   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 1       | 1387  | 0     | 3.80   |
| Toshiba   | DT01ACA100         | 1 TB   | 3       | 1357  | 0     | 3.72   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 1       | 2421  | 1     | 3.32   |
| Seagate   | ST9250315AS        | 250 GB | 1       | 1192  | 0     | 3.27   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 3       | 1753  | 121   | 3.21   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 1       | 1146  | 0     | 3.14   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 2       | 1098  | 0     | 3.01   |
| Seagate   | ST320VT000-1BS14C  | 320 GB | 1       | 1083  | 0     | 2.97   |
| Seagate   | ST3160023A         | 160 GB | 1       | 1056  | 0     | 2.89   |
| Seagate   | ST3250312AS        | 250 GB | 1       | 1039  | 0     | 2.85   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 4       | 1018  | 0     | 2.79   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 2       | 890   | 0     | 2.44   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 1       | 864   | 0     | 2.37   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 1       | 860   | 0     | 2.36   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 856   | 0     | 2.35   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 4       | 1070  | 2     | 2.21   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 2       | 802   | 0     | 2.20   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 1       | 799   | 0     | 2.19   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 1       | 765   | 0     | 2.10   |
| Toshiba   | HDWQ140            | 4 TB   | 2       | 742   | 0     | 2.03   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 3       | 1143  | 51    | 1.97   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 1       | 707   | 0     | 1.94   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 1       | 658   | 0     | 1.80   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 625   | 0     | 1.71   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 1       | 611   | 0     | 1.68   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 1       | 598   | 0     | 1.64   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 1       | 596   | 0     | 1.63   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 1       | 563   | 0     | 1.54   |
| Hitachi   | HTS725050A7E630    | 500 GB | 1       | 535   | 0     | 1.47   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 1       | 517   | 0     | 1.42   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 1       | 517   | 0     | 1.42   |
| Toshiba   | MQ01ABD100         | 1 TB   | 1       | 463   | 0     | 1.27   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 1       | 455   | 0     | 1.25   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 2       | 430   | 0     | 1.18   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 1       | 429   | 0     | 1.18   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 1       | 424   | 0     | 1.16   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 1       | 422   | 0     | 1.16   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 7       | 458   | 1     | 1.11   |
| Seagate   | ST380811AS         | 80 GB  | 1       | 383   | 0     | 1.05   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 1       | 347   | 0     | 0.95   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 2       | 1571  | 6     | 0.77   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 1       | 263   | 0     | 0.72   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 1       | 2015  | 7     | 0.69   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 1       | 239   | 0     | 0.66   |
| HGST      | HTS541075A7E630    | 752 GB | 2       | 321   | 507   | 0.62   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 1       | 213   | 0     | 0.59   |
| HGST      | HTS721010A9E630    | 1 TB   | 2       | 213   | 0     | 0.59   |
| HGST      | HTS725050A7E630    | 500 GB | 1       | 175   | 0     | 0.48   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 1       | 327   | 1     | 0.45   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 3       | 134   | 0     | 0.37   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 1       | 111   | 0     | 0.31   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 2       | 277   | 4     | 0.30   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 1       | 1338  | 12    | 0.28   |
| Toshiba   | HDWD120            | 2 TB   | 1       | 77    | 0     | 0.21   |
| Toshiba   | HDWD110            | 1 TB   | 1       | 62    | 0     | 0.17   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 1       | 55    | 0     | 0.15   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 1       | 52    | 0     | 0.14   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 2       | 227   | 505   | 0.14   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 1       | 44    | 0     | 0.12   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 1       | 41    | 0     | 0.11   |
| Toshiba   | MQ04ABF100         | 1 TB   | 2       | 92    | 2     | 0.09   |
| Samsung   | HM320JI            | 320 GB | 1       | 258   | 9     | 0.07   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 1       | 24    | 0     | 0.07   |
| Toshiba   | MK5061GSYN         | 500 GB | 1       | 15    | 0     | 0.04   |
| Hitachi   | HTS543212L9A300    | 120 GB | 1       | 1158  | 88    | 0.04   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 1       | 1511  | 220   | 0.02   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 16      | 3     | 0     | 0.01   |
| Seagate   | ST3500514NS        | 500 GB | 1       | 205   | 103   | 0.01   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 1       | 161   | 144   | 0.00   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 1       | 165   | 372   | 0.00   |
| Seagate   | ST9500420AS        | 500 GB | 1       | 315   | 738   | 0.00   |
| Hitachi   | HTS721060G9AT00    | 64 GB  | 1       | 0     | 37    | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Seagate   | Barracuda ATA V        | 1      | 1       | 5214  | 0     | 14.29  |
| WDC       | Caviar SE              | 1      | 4       | 5313  | 4     | 11.14  |
| Seagate   | Barracuda ES           | 1      | 1       | 4005  | 0     | 10.97  |
| Hitachi   | Deskstar 7K500         | 1      | 1       | 3763  | 0     | 10.31  |
| WDC       | RE4                    | 1      | 4       | 3039  | 0     | 8.33   |
| Hitachi   | Deskstar T7K500        | 1      | 1       | 2680  | 0     | 7.34   |
| WDC       | RE3                    | 1      | 1       | 2374  | 0     | 6.51   |
| WDC       | Caviar Black           | 4      | 7       | 2528  | 3     | 6.11   |
| Hitachi   | Deskstar 7K160         | 1      | 1       | 2187  | 0     | 5.99   |
| Seagate   | Constellation ES.3     | 1      | 3       | 1988  | 0     | 5.45   |
| WDC       | Green                  | 8      | 13      | 1982  | 0     | 5.43   |
| Samsung   | SpinPoint T166         | 1      | 4       | 3871  | 3     | 5.15   |
| Seagate   | Constellation CS       | 1      | 1       | 1848  | 0     | 5.06   |
| Hitachi   | Ultrastar 7K3000       | 2      | 3       | 1834  | 0     | 5.03   |
| Seagate   | Barracuda 7200.10      | 2      | 2       | 1825  | 0     | 5.00   |
| Seagate   | Barracuda 7200.12      | 4      | 5       | 1747  | 0     | 4.79   |
| WDC       | Caviar Green           | 2      | 5       | 2698  | 3     | 4.64   |
| Toshiba   | 3.5" HDD DT01ACA       | 2      | 6       | 1675  | 0     | 4.59   |
| Seagate   | Constellation.2 (SATA) | 1      | 1       | 1630  | 0     | 4.47   |
| Seagate   | Desktop HDD.15         | 2      | 3       | 1194  | 0     | 3.27   |
| Seagate   | Momentus 5400.6        | 1      | 1       | 1192  | 0     | 3.27   |
| WDC       | Blue                   | 11     | 16      | 1178  | 0     | 3.23   |
| Hitachi   | Ultrastar A7K2000      | 1      | 3       | 1753  | 121   | 3.21   |
| Seagate   | Unknown                | 1      | 1       | 1083  | 0     | 2.97   |
| Seagate   | Barracuda 7200.7 an... | 1      | 1       | 1056  | 0     | 2.89   |
| WDC       | Elements / My Passport | 2      | 2       | 858   | 0     | 2.35   |
| WDC       | Red Pro                | 1      | 2       | 802   | 0     | 2.20   |
| Seagate   | Barracuda Compute      | 1      | 1       | 765   | 0     | 2.10   |
| Toshiba   | 3.5" HDD N300          | 1      | 2       | 742   | 0     | 2.03   |
| WDC       | Red                    | 6      | 19      | 879   | 1     | 2.03   |
| Seagate   | Barracuda 7200.14 (AF) | 1      | 3       | 1143  | 51    | 1.97   |
| Fujitsu   | MJA BH                 | 1      | 1       | 707   | 0     | 1.94   |
| Seagate   | NAS HDD                | 1      | 1       | 625   | 0     | 1.71   |
| Seagate   | Surveillance           | 1      | 1       | 596   | 0     | 1.63   |
| Hitachi   | Travelstar Z7K500      | 1      | 1       | 535   | 0     | 1.47   |
| WDC       | Scorpio Blue           | 2      | 2       | 520   | 0     | 1.43   |
| Hitachi   | Travelstar 5K160       | 1      | 1       | 517   | 0     | 1.42   |
| WDC       | HGST Ultrastar He10    | 1      | 1       | 517   | 0     | 1.42   |
| Toshiba   | 2.5" HDD MQ01ABD       | 1      | 1       | 463   | 0     | 1.27   |
| WDC       | RE2                    | 1      | 1       | 455   | 0     | 1.25   |
| WDC       | Caviar Blue            | 1      | 1       | 424   | 0     | 1.16   |
| Seagate   | Laptop HDD             | 2      | 3       | 534   | 337   | 1.14   |
| Seagate   | Barracuda 7200.9       | 1      | 1       | 383   | 0     | 1.05   |
| Seagate   | SpinPoint M8 (AF)      | 2      | 2       | 280   | 0     | 0.77   |
| WDC       | RE4-GP                 | 1      | 2       | 1571  | 6     | 0.77   |
| Seagate   | Barracuda 2.5 5400     | 3      | 4       | 240   | 0     | 0.66   |
| HGST      | Travelstar Z5K1000     | 1      | 2       | 321   | 507   | 0.62   |
| HGST      | Travelstar 7K1000      | 1      | 2       | 213   | 0     | 0.59   |
| HGST      | Travelstar Z7K500      | 1      | 1       | 175   | 0     | 0.48   |
| WDC       | Black                  | 1      | 1       | 327   | 1     | 0.45   |
| WDC       | Black Mobile           | 2      | 2       | 152   | 0     | 0.42   |
| Seagate   | Mobile HDD             | 1      | 1       | 111   | 0     | 0.31   |
| Hitachi   | Travelstar 4K120       | 1      | 1       | 1338  | 12    | 0.28   |
| Toshiba   | P300                   | 2      | 2       | 69    | 0     | 0.19   |
| Seagate   | IronWolf               | 3      | 18      | 53    | 0     | 0.15   |
| Hitachi   | Ultrastar A7K1000      | 1      | 1       | 52    | 0     | 0.14   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 2       | 92    | 2     | 0.09   |
| Samsung   | SpinPoint M6           | 1      | 1       | 258   | 9     | 0.07   |
| WDC       | Blue Mobile            | 1      | 1       | 24    | 0     | 0.07   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 1      | 1       | 15    | 0     | 0.04   |
| Hitachi   | Travelstar 5K320       | 1      | 1       | 1158  | 88    | 0.04   |
| Hitachi   | Deskstar 7K1000.C      | 1      | 1       | 1511  | 220   | 0.02   |
| Seagate   | Constellation ES (S... | 1      | 1       | 205   | 103   | 0.01   |
| Seagate   | BarraCuda 3.5          | 1      | 1       | 161   | 144   | 0.00   |
| WDC       | Gold                   | 1      | 1       | 165   | 372   | 0.00   |
| Seagate   | Momentus 7200.4        | 1      | 1       | 315   | 738   | 0.00   |
| Hitachi   | Travelstar 7K100       | 1      | 1       | 0     | 37    | 0.00   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Samsung     | 2      | 5       | 3148  | 4     | 4.13   |
| WDC         | 48     | 85      | 1624  | 6     | 3.88   |
| Hitachi     | 13     | 16      | 1531  | 45    | 3.23   |
| Toshiba     | 8      | 14      | 881   | 1     | 2.39   |
| Seagate     | 35     | 58      | 838   | 38    | 2.19   |
| Fujitsu     | 1      | 1       | 707   | 0     | 1.94   |
| HGST        | 3      | 5       | 248   | 203   | 0.58   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

See complete list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Intel     | SSDSA2CT040G3      | 40 GB  | 1       | 2994  | 0     | 8.20   |
| Samsung   | SSD 840 Series     | 120 GB | 1       | 2655  | 0     | 7.28   |
| OCZ       | AGILITY3           | 120 GB | 1       | 2119  | 0     | 5.81   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 1       | 1425  | 0     | 3.91   |
| Intel     | SSDSC2BW240H6      | 240 GB | 1       | 1258  | 0     | 3.45   |
| SanDisk   | Ultra II           | 960 GB | 2       | 1202  | 0     | 3.29   |
| SuperM... | SSD                | 16 GB  | 1       | 1176  | 0     | 3.22   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 1       | 2157  | 1     | 2.96   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 1059  | 0     | 2.90   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 2       | 1042  | 0     | 2.86   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 1       | 1009  | 0     | 2.77   |
| Samsung   | SSD 850 EVO        | 250 GB | 9       | 1003  | 0     | 2.75   |
| Crucial   | CT240M500SSD3      | 240 GB | 1       | 917   | 0     | 2.51   |
| Kingston  | SUV400S37240G      | 240 GB | 1       | 833   | 0     | 2.28   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 1       | 811   | 0     | 2.22   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 4       | 778   | 0     | 2.13   |
| Apple     | SSD TS256C         | 256 GB | 1       | 752   | 0     | 2.06   |
| Samsung   | SSD 750 EVO        | 250 GB | 1       | 734   | 0     | 2.01   |
| Kingston  | SV300S37A120G      | 120 GB | 1       | 709   | 0     | 1.94   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 1       | 697   | 0     | 1.91   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 1       | 683   | 0     | 1.87   |
| SanDisk   | Ultra II           | 480 GB | 1       | 676   | 0     | 1.85   |
| Samsung   | SSD 850 EVO        | 500 GB | 3       | 676   | 0     | 1.85   |
| Samsung   | SSD 850 EVO        | 1 TB   | 3       | 1196  | 1     | 1.80   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 1       | 607   | 0     | 1.66   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 1       | 589   | 0     | 1.61   |
| Hoodisk   | SSD                | 32 GB  | 1       | 587   | 0     | 1.61   |
| Kingston  | SUV500MS240G       | 240 GB | 1       | 580   | 0     | 1.59   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 1       | 544   | 0     | 1.49   |
| Crucial   | CT250MX200SSD1     | 250 GB | 2       | 517   | 0     | 1.42   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 1       | 516   | 0     | 1.42   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 1       | 516   | 0     | 1.41   |
| Plextor   | PX-128M7VC         | 128 GB | 1       | 483   | 0     | 1.32   |
| SPCC      | SSD                | 64 GB  | 1       | 482   | 0     | 1.32   |
| Samsung   | SSD 850 PRO        | 256 GB | 1       | 467   | 0     | 1.28   |
| AEGO      | SSD                | 120 GB | 1       | 445   | 0     | 1.22   |
| Samsung   | SSD PM830 FDE 2... | 256 GB | 1       | 440   | 0     | 1.21   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 1       | 424   | 0     | 1.16   |
| Samsung   | SSD 850 EVO        | 120 GB | 1       | 358   | 0     | 0.98   |
| Intel     | SSDSC2BB480G7      | 480 GB | 1       | 703   | 1     | 0.96   |
| Samsung   | SSD 860 EVO        | 1 TB   | 2       | 348   | 0     | 0.96   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 1       | 3057  | 8     | 0.93   |
| Samsung   | SSD 860 EVO        | 500 GB | 4       | 327   | 0     | 0.90   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 1       | 274   | 0     | 0.75   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 1       | 246   | 0     | 0.68   |
| Samsung   | SSD 840 PRO Series | 256 GB | 1       | 243   | 0     | 0.67   |
| SPCC      | SSD                | 120 GB | 1       | 228   | 0     | 0.63   |
| Samsung   | SSD 840 Series     | 250 GB | 1       | 227   | 0     | 0.62   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 1       | 196   | 0     | 0.54   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 1       | 188   | 0     | 0.52   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 1       | 162   | 0     | 0.44   |
| Samsung   | SSD 860 QVO        | 1 TB   | 1       | 150   | 0     | 0.41   |
| Transcend | TS240GMTS420S      | 240 GB | 1       | 145   | 0     | 0.40   |
| Samsung   | SSD 860 QVO        | 4 TB   | 1       | 141   | 0     | 0.39   |
| KingSpec  | NT-128             | 128 GB | 1       | 140   | 0     | 0.38   |
| Kingston  | SA400S37480G       | 480 GB | 1       | 135   | 0     | 0.37   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 1       | 129   | 0     | 0.35   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 1       | 115   | 0     | 0.32   |
| Verbatim  | Vi500 S3 480GB SSD | 480 GB | 1       | 115   | 0     | 0.32   |
| Crucial   | CT120BX300SSD1     | 120 GB | 1       | 108   | 0     | 0.30   |
| Crucial   | CT525MX300SSD1     | 528 GB | 1       | 300   | 2     | 0.27   |
| Intel     | SSDSC2BW240A4      | 240 GB | 1       | 89    | 0     | 0.24   |
| Samsung   | SSD 860 QVO        | 2 TB   | 1       | 88    | 0     | 0.24   |
| Toshiba   | TR200              | 240 GB | 1       | 77    | 0     | 0.21   |
| SPCC      | SSD                | 256 GB | 1       | 71    | 0     | 0.19   |
| Samsung   | SSD 860 EVO        | 4 TB   | 1       | 68    | 0     | 0.19   |
| Samsung   | MZMTE1T0HMJH-00000 | 1 TB   | 1       | 59    | 0     | 0.16   |
| Crucial   | CT500MX200SSD1     | 500 GB | 1       | 54    | 0     | 0.15   |
| Kingston  | SUV500MS480G       | 480 GB | 2       | 49    | 0     | 0.14   |
| Corsair   | Force LS SSD       | 64 GB  | 1       | 39    | 0     | 0.11   |
| ADATA     | SU750              | 256 GB | 1       | 36    | 0     | 0.10   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 1       | 107   | 2     | 0.10   |
| Kingston  | SA400S37120G       | 120 GB | 1       | 22    | 0     | 0.06   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 1       | 21    | 0     | 0.06   |
| Crucial   | CT120BX500SSD1     | 120 GB | 1       | 14    | 0     | 0.04   |
| Leven     | JAJS600M512C       | 512 GB | 1       | 9     | 0     | 0.03   |
| Transcend | TS128GMTS430S      | 128 GB | 1       | 8     | 0     | 0.02   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 25      | 8     | 0     | 0.02   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 1       | 144   | 89    | 0.00   |
| Lite-On   | LCH-128V2S         | 128 GB | 1       | 1     | 0     | 0.00   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 39    | 1010  | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Intel     | 320 Series SSDs        | 1      | 1       | 2994  | 0     | 8.20   |
| OCZ       | SandForce Driven SSDs  | 1      | 1       | 2119  | 0     | 5.81   |
| Intel     | 53x and Pro 2500 Se... | 1      | 1       | 1258  | 0     | 3.45   |
| SuperM... | Silicon Motion base... | 1      | 1       | 1176  | 0     | 3.22   |
| Crucial   | Unknown                | 1      | 2       | 1042  | 0     | 2.86   |
| Toshiba   | HG6 Series SSD         | 1      | 1       | 1009  | 0     | 2.77   |
| Intel     | 520 Series SSDs        | 2      | 2       | 850   | 0     | 2.33   |
| Kingston  | SSDNow UV400           | 1      | 1       | 833   | 0     | 2.28   |
| SanDisk   | Marvell based SanDi... | 3      | 4       | 831   | 0     | 2.28   |
| Micron    | 5100 Pro / 5200 SSDs   | 1      | 4       | 778   | 0     | 2.13   |
| Apple     | JMicron based SSDs     | 1      | 1       | 752   | 0     | 2.06   |
| Kingston  | SandForce Driven SSDs  | 1      | 1       | 709   | 0     | 1.94   |
| Samsung   | Samsung based SSDs     | 22     | 38      | 734   | 1     | 1.82   |
| Crucial   | RealSSD m4/C400/P400   | 1      | 1       | 589   | 0     | 1.61   |
| Hoodisk   | Phison Driven OEM SSDs | 1      | 1       | 587   | 0     | 1.61   |
| Kingston  | Phison Driven SSDs     | 3      | 4       | 569   | 0     | 1.56   |
| Plextor   | Unknown                | 1      | 1       | 483   | 0     | 1.32   |
| AEGO      | Unknown                | 1      | 1       | 445   | 0     | 1.22   |
| SanDisk   | Unknown                | 1      | 1       | 424   | 0     | 1.16   |
| Crucial   | BX/MX1/2/3/500, M5/... | 7      | 8       | 405   | 1     | 1.04   |
| Intel     | 730 and DC S35x0/36... | 1      | 1       | 703   | 1     | 0.96   |
| Intel     | X18-M/X25-M/X25-V G... | 1      | 1       | 3057  | 8     | 0.93   |
| SPCC      | Phison Driven OEM SSDs | 3      | 3       | 260   | 0     | 0.71   |
| Kingston  | SSDNow UV400/500       | 2      | 3       | 226   | 0     | 0.62   |
| KingSpec  | Unknown                | 1      | 1       | 140   | 0     | 0.38   |
| Verbatim  | Unknown                | 1      | 1       | 115   | 0     | 0.32   |
| Samsung   | Unknown                | 4      | 4       | 112   | 0     | 0.31   |
| Intel     | 53x and Pro 1500/25... | 1      | 1       | 89    | 0     | 0.24   |
| Toshiba   | Unknown                | 1      | 1       | 77    | 0     | 0.21   |
| Transcend | Silicon Motion base... | 2      | 2       | 77    | 0     | 0.21   |
| Micron    | BX/MX1/2/3/500, M5/... | 2      | 2       | 68    | 0     | 0.19   |
| Corsair   | SandForce Driven SSDs  | 1      | 1       | 39    | 0     | 0.11   |
| ADATA     | Unknown                | 1      | 1       | 36    | 0     | 0.10   |
| WDC       | Blue and Green SSDs    | 3      | 27      | 20    | 0     | 0.06   |
| Intel     | Unknown                | 2      | 2       | 126   | 46    | 0.05   |
| Leven     | Unknown                | 1      | 1       | 9     | 0     | 0.03   |
| Lite-On   | Unknown                | 1      | 1       | 1     | 0     | 0.00   |
| Intel     | 540 Series SSDs        | 1      | 1       | 39    | 1010  | 0.00   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| OCZ         | 1      | 1       | 2119  | 0     | 5.81   |
| SuperMicro  | 1      | 1       | 1176  | 0     | 3.22   |
| Apple       | 1      | 1       | 752   | 0     | 2.06   |
| SanDisk     | 4      | 5       | 750   | 0     | 2.06   |
| Intel       | 10     | 10      | 1009  | 111   | 1.86   |
| Samsung     | 26     | 42      | 675   | 1     | 1.67   |
| Hoodisk     | 1      | 1       | 587   | 0     | 1.61   |
| Toshiba     | 2      | 2       | 543   | 0     | 1.49   |
| Micron      | 3      | 6       | 542   | 0     | 1.49   |
| Crucial     | 9      | 11      | 537   | 1     | 1.42   |
| Kingston    | 7      | 9       | 499   | 0     | 1.37   |
| Plextor     | 1      | 1       | 483   | 0     | 1.32   |
| AEGO        | 1      | 1       | 445   | 0     | 1.22   |
| SPCC        | 3      | 3       | 260   | 0     | 0.71   |
| KingSpec    | 1      | 1       | 140   | 0     | 0.38   |
| Verbatim    | 1      | 1       | 115   | 0     | 0.32   |
| Transcend   | 2      | 2       | 77    | 0     | 0.21   |
| Corsair     | 1      | 1       | 39    | 0     | 0.11   |
| ADATA       | 1      | 1       | 36    | 0     | 0.10   |
| WDC         | 3      | 27      | 20    | 0     | 0.06   |
| Leven       | 1      | 1       | 9     | 0     | 0.03   |
| Lite-On     | 1      | 1       | 1     | 0     | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

See complete list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Samsung   | MZVPV256HDGL-000L7 | 256 GB | 1       | 915   | 0     | 2.51   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 1       | 405   | 0     | 1.11   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 1       | 109   | 0     | 0.30   |
| Samsung   | SSD 960 EVO        | 1 TB   | 1       | 154   | 3     | 0.11   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days   — avg. days per sample,
Err    — avg. errors per sample,
MTBF   — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Samsung     | 2      | 2       | 535   | 2     | 1.31   |
| Intel       | 1      | 1       | 405   | 0     | 1.11   |
| Corsair     | 1      | 1       | 109   | 0     | 0.30   |

