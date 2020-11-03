HDD/SSD Reliability Test
========================

This is a project to estimate reliability of HDD/SSD drives by
the analysis of SMART data collected by BSD users at https://bsd-hardware.info. The
primary aim of the project is to find drives with longest power-on hours (POH) and
minimal number of errors, i.e. maximal MTBF (mean time between failures).

Everyone can contribute to this report by uploading probes of their computers by
the [hw-probe](https://github.com/linuxhw/hw-probe/blob/master/INSTALL.BSD.md) tool:

    hw-probe -all -upload

Total drives: 1548.

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
| WDC       | WD800JD-08MSA1     | 80 GB  | 1       | 4687  | 0     | 12.84  |
| WDC       | WD1600AAJS-00PSA0  | 160 GB | 1       | 4208  | 0     | 11.53  |
| WDC       | WD1600JD-00GBB0    | 160 GB | 4       | 5313  | 4     | 11.14  |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 2       | 3969  | 0     | 10.88  |
| WDC       | WD10EACS-00D6B0    | 1 TB   | 1       | 3820  | 0     | 10.47  |
| Hitachi   | HDT721010SLA360    | 1 TB   | 1       | 3782  | 0     | 10.36  |
| Hitachi   | HDS725050KLA360    | 500 GB | 1       | 3763  | 0     | 10.31  |
| WDC       | WD2001FASS-00U0B0  | 2 TB   | 2       | 3704  | 0     | 10.15  |
| Hitachi   | HDT721032SLA360    | 320 GB | 1       | 3534  | 0     | 9.68   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 4       | 3472  | 0     | 9.51   |
| Samsung   | HD753LJ            | 752 GB | 1       | 3468  | 0     | 9.50   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 1       | 3368  | 0     | 9.23   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 3       | 3329  | 0     | 9.12   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 6       | 3085  | 0     | 8.45   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 4       | 3039  | 0     | 8.33   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 3       | 2977  | 0     | 8.16   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 1       | 2864  | 0     | 7.85   |
| WDC       | WD400BB-00GFA0     | 40 GB  | 1       | 2808  | 0     | 7.69   |
| Hitachi   | HUA7250SBSUN500G   | 500 GB | 2       | 2785  | 0     | 7.63   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 2       | 2745  | 0     | 7.52   |
| Seagate   | ST3500630NS        | 500 GB | 3       | 2715  | 0     | 7.44   |
| Seagate   | ST32000645NS       | 2 TB   | 1       | 2713  | 0     | 7.43   |
| Hitachi   | HDT725025VLA380    | 250 GB | 1       | 2680  | 0     | 7.34   |
| WDC       | WD3200AAKX-00ERMA0 | 320 GB | 1       | 2660  | 0     | 7.29   |
| Hitachi   | HTS542525K9SA00    | 250 GB | 1       | 2643  | 0     | 7.24   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 1       | 2461  | 0     | 6.74   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 1       | 2414  | 0     | 6.61   |
| WDC       | WD30EZRX-00AZ6B0   | 3 TB   | 1       | 2343  | 0     | 6.42   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 2       | 2320  | 0     | 6.36   |
| Samsung   | HD103SJ            | 1 TB   | 3       | 2850  | 1     | 6.29   |
| Seagate   | ST3160318AS        | 160 GB | 1       | 2290  | 0     | 6.27   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 3       | 2281  | 0     | 6.25   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 7       | 2259  | 0     | 6.19   |
| WDC       | WD10EARX-00N0YB0   | 1 TB   | 1       | 2233  | 0     | 6.12   |
| Hitachi   | HDS721616PLAT80    | 160 GB | 1       | 2187  | 0     | 5.99   |
| WDC       | WD1001FAES-75W7A0  | 1 TB   | 1       | 2183  | 0     | 5.98   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 3       | 2169  | 0     | 5.94   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 1       | 2162  | 0     | 5.92   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 5       | 2119  | 0     | 5.81   |
| Hitachi   | HDS728080PLA380    | 82 GB  | 1       | 2086  | 0     | 5.72   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 1       | 2024  | 0     | 5.55   |
| Toshiba   | DT01ACA200         | 2 TB   | 3       | 1992  | 0     | 5.46   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 3       | 1988  | 0     | 5.45   |
| HGST      | HUS724020ALA640    | 2 TB   | 4       | 1983  | 0     | 5.43   |
| Toshiba   | MQ01ABD100H        | 1 TB   | 1       | 1970  | 0     | 5.40   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 8       | 2216  | 1     | 5.39   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 2       | 1944  | 0     | 5.33   |
| WDC       | WD10EZEX-08M2NA0   | 1 TB   | 2       | 1933  | 0     | 5.30   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 5       | 2167  | 1     | 5.27   |
| Seagate   | ST3320620A         | 320 GB | 1       | 1913  | 0     | 5.24   |
| Samsung   | HD204UI            | 2 TB   | 3       | 1849  | 0     | 5.07   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 1       | 1848  | 0     | 5.06   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 3       | 2230  | 1     | 5.06   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 1       | 1827  | 0     | 5.01   |
| WDC       | WD3000GLFS-01F8U0  | 304 GB | 1       | 1824  | 0     | 5.00   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 8       | 2159  | 1     | 5.00   |
| HGST      | HUH728060ALE600    | 6 TB   | 1       | 1820  | 0     | 4.99   |
| WDC       | WD6400AAKS-00A7B0  | 640 GB | 1       | 1819  | 0     | 4.98   |
| Samsung   | HD501LJ            | 500 GB | 5       | 3372  | 2     | 4.87   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 4       | 2204  | 91    | 4.84   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 1       | 1673  | 0     | 4.58   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 2       | 1670  | 0     | 4.58   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 1       | 1647  | 0     | 4.51   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 2       | 1644  | 0     | 4.51   |
| Seagate   | ST3250318AS        | 250 GB | 1       | 1636  | 0     | 4.48   |
| Toshiba   | MG03ACA200         | 2 TB   | 5       | 1631  | 0     | 4.47   |
| Seagate   | ST91000640NS       | 1 TB   | 1       | 1630  | 0     | 4.47   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 4       | 1546  | 0     | 4.24   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 1       | 1543  | 0     | 4.23   |
| HGST      | HDN724030ALE640    | 3 TB   | 2       | 1543  | 0     | 4.23   |
| Seagate   | ST33000651AS       | 3 TB   | 1       | 1539  | 0     | 4.22   |
| Toshiba   | MG04ACA400E        | 4 TB   | 2       | 1535  | 0     | 4.21   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 3       | 1514  | 0     | 4.15   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 4       | 1513  | 0     | 4.15   |
| Seagate   | ST31000524AS       | 1 TB   | 3       | 1501  | 0     | 4.11   |
| WDC       | WD7500BMVW-11AJGS4 | 752 GB | 1       | 1500  | 0     | 4.11   |
| Seagate   | ST3500412AS        | 500 GB | 1       | 1499  | 0     | 4.11   |
| WDC       | WD15EADS-00P8B0    | 1.5 TB | 3       | 3153  | 4     | 4.05   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 1       | 1475  | 0     | 4.04   |
| WDC       | WD2000FYYX         | 2 TB   | 4       | 1466  | 0     | 4.02   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 3       | 1450  | 0     | 3.97   |
| WDC       | WD10PURX-64D85Y0   | 1 TB   | 1       | 1445  | 0     | 3.96   |
| Seagate   | ST9250410AS        | 250 GB | 1       | 1400  | 0     | 3.84   |
| Samsung   | HD502HJ            | 500 GB | 1       | 1380  | 0     | 3.78   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 1       | 1376  | 0     | 3.77   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 4       | 1797  | 28    | 3.71   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 3       | 1348  | 0     | 3.69   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 3       | 2182  | 874   | 3.68   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 26      | 1583  | 1     | 3.66   |
| Hitachi   | HDS721032CLA362    | 320 GB | 1       | 1323  | 0     | 3.63   |
| WDC       | WD5000BMVV-11A1CS0 | 500 GB | 1       | 1308  | 0     | 3.59   |
| Toshiba   | DT01ACA300         | 3 TB   | 8       | 1606  | 129   | 3.56   |
| WDC       | WD8001FFWX-68J1UN0 | 8 TB   | 1       | 1296  | 0     | 3.55   |
| WDC       | WD2500AAKX-07U6AA0 | 250 GB | 1       | 1289  | 0     | 3.53   |
| Seagate   | ST3500413AS        | 500 GB | 6       | 1721  | 2     | 3.53   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 6       | 1267  | 0     | 3.47   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 2       | 1237  | 0     | 3.39   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 3       | 1220  | 0     | 3.34   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 1       | 1215  | 0     | 3.33   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 1       | 3610  | 2     | 3.30   |
| Seagate   | ST320LM001 HN-M... | 320 GB | 2       | 1189  | 0     | 3.26   |
| WDC       | WD3750LMCW-11D9GS3 | 375 GB | 1       | 1179  | 0     | 3.23   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 1       | 1158  | 0     | 3.17   |
| Samsung   | SP2504C            | 250 GB | 1       | 1158  | 0     | 3.17   |
| HGST      | HDN724040ALE640    | 4 TB   | 8       | 1683  | 101   | 3.15   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 1       | 1146  | 0     | 3.14   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 1       | 1142  | 0     | 3.13   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 4       | 1463  | 164   | 3.09   |
| Seagate   | ST500DM009-2DM14C  | 500 GB | 1       | 1122  | 0     | 3.08   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 1       | 1107  | 0     | 3.03   |
| Seagate   | ST320VT000-1BS14C  | 320 GB | 1       | 1083  | 0     | 2.97   |
| Toshiba   | DT01ACA050         | 500 GB | 4       | 1146  | 1     | 2.96   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 1       | 1076  | 0     | 2.95   |
| Toshiba   | MQ01UBB200         | 2 TB   | 1       | 1067  | 0     | 2.93   |
| Seagate   | ST3250312AS        | 250 GB | 2       | 1063  | 0     | 2.91   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 13      | 1142  | 1     | 2.91   |
| Seagate   | ST3160023A         | 160 GB | 1       | 1056  | 0     | 2.89   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 1       | 1051  | 0     | 2.88   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 5       | 1032  | 0     | 2.83   |
| Toshiba   | MC04ACA400E        | 4 TB   | 2       | 1023  | 0     | 2.80   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 8       | 1090  | 1     | 2.80   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 2       | 1018  | 0     | 2.79   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 4       | 1018  | 0     | 2.79   |
| ExcelStor | J8160              | 164 GB | 2       | 1015  | 0     | 2.78   |
| Hitachi   | HTS545025B9SA02    | 250 GB | 1       | 1008  | 0     | 2.76   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 1       | 1007  | 0     | 2.76   |
| HGST      | HDN728080ALE604    | 8 TB   | 1       | 1005  | 0     | 2.75   |
| Seagate   | ST380817AS         | 80 GB  | 1       | 997   | 0     | 2.73   |
| Toshiba   | HDWE150            | 5 TB   | 6       | 1186  | 5     | 2.73   |
| Seagate   | ST380013AS         | 80 GB  | 1       | 2943  | 2     | 2.69   |
| Seagate   | ST4000NE0025-2E... | 4 TB   | 2       | 960   | 0     | 2.63   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 7       | 1631  | 174   | 2.57   |
| Toshiba   | MQ04UBD200         | 2 TB   | 1       | 906   | 0     | 2.48   |
| Samsung   | HD103UJ            | 1 TB   | 5       | 1844  | 33    | 2.48   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 2       | 890   | 0     | 2.44   |
| WDC       | WD2500JS-75NCB2    | 250 GB | 2       | 889   | 0     | 2.44   |
| Toshiba   | DT01ACA100         | 1 TB   | 10      | 883   | 0     | 2.42   |
| Seagate   | ST500DM002-1ER14C  | 500 GB | 1       | 882   | 0     | 2.42   |
| Seagate   | ST3250310AS        | 250 GB | 1       | 881   | 0     | 2.42   |
| WDC       | WD1600AAJS-60B4A0  | 160 GB | 1       | 872   | 0     | 2.39   |
| Seagate   | ST3320620AS        | 320 GB | 2       | 1023  | 86    | 2.38   |
| HGST      | HTS541010A9E680    | 1 TB   | 3       | 869   | 0     | 2.38   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 2       | 861   | 0     | 2.36   |
| WDC       | WD20NMVW-11AV3S2   | 2 TB   | 1       | 860   | 0     | 2.36   |
| Seagate   | ST320410A          | 20 GB  | 1       | 2579  | 2     | 2.36   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 856   | 0     | 2.35   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 1       | 828   | 0     | 2.27   |
| WDC       | WD10PURZ-85U8XY0   | 1 TB   | 1       | 819   | 0     | 2.25   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 1       | 816   | 0     | 2.24   |
| Samsung   | HD154UI            | 1.5 TB | 2       | 2245  | 75    | 2.21   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 2       | 802   | 0     | 2.20   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 1       | 799   | 0     | 2.19   |
| WDC       | WD10EZEX-07WN4A0   | 1 TB   | 1       | 790   | 0     | 2.17   |
| WDC       | WD1200BEVT-22ZCT0  | 120 GB | 1       | 786   | 0     | 2.15   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 19      | 1116  | 72    | 2.15   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 6       | 976   | 1     | 2.14   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 1       | 769   | 0     | 2.11   |
| Seagate   | ST3500312CS        | 500 GB | 2       | 744   | 0     | 2.04   |
| Seagate   | ST5000DM000-1FK178 | 5 TB   | 2       | 731   | 0     | 2.01   |
| Seagate   | ST31000424CS       | 1 TB   | 1       | 721   | 0     | 1.98   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 6       | 829   | 3     | 1.95   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 1       | 710   | 0     | 1.95   |
| WDC       | WD5000LPVT-75G33T0 | 500 GB | 1       | 708   | 0     | 1.94   |
| Fujitsu   | MJA2160BH FFS G1   | 160 GB | 1       | 707   | 0     | 1.94   |
| WDC       | WD80EFAX-68LHPN0   | 8 TB   | 3       | 705   | 0     | 1.93   |
| Seagate   | ST3500418AS        | 500 GB | 4       | 784   | 1     | 1.92   |
| Seagate   | ST2000NM0011       | 2 TB   | 1       | 2080  | 2     | 1.90   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 11      | 692   | 0     | 1.90   |
| Seagate   | ST3320620NS        | 320 GB | 1       | 2076  | 2     | 1.90   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 3       | 687   | 0     | 1.88   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 1       | 678   | 0     | 1.86   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 2       | 674   | 0     | 1.85   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 1       | 658   | 0     | 1.80   |
| Toshiba   | HDWD130            | 3 TB   | 4       | 656   | 0     | 1.80   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 7       | 975   | 166   | 1.78   |
| Hitachi   | HTS723225L9A360    | 250 GB | 1       | 644   | 0     | 1.77   |
| Fujitsu   | MJA2160BH G2       | 160 GB | 1       | 633   | 0     | 1.74   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 11      | 629   | 0     | 1.72   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 625   | 0     | 1.71   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 3       | 624   | 0     | 1.71   |
| WDC       | WD2500AAKX-19U6AA0 | 250 GB | 1       | 613   | 0     | 1.68   |
| WDC       | WD2500LPCX-24C6HT0 | 250 GB | 1       | 608   | 0     | 1.67   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 1       | 598   | 0     | 1.64   |
| Seagate   | ST9250315AS        | 250 GB | 2       | 928   | 506   | 1.64   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 1       | 596   | 0     | 1.63   |
| Toshiba   | MQ04UBF100         | 1 TB   | 1       | 592   | 0     | 1.62   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 1       | 579   | 0     | 1.59   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 5       | 574   | 0     | 1.57   |
| WDC       | WD2500BEVS-08VAT2  | 250 GB | 1       | 573   | 0     | 1.57   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 27      | 583   | 1     | 1.56   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 2       | 566   | 0     | 1.55   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 1       | 563   | 0     | 1.54   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 3       | 551   | 0     | 1.51   |
| Samsung   | HD160JJ-P          | 160 GB | 1       | 547   | 0     | 1.50   |
| Hitachi   | HTS725050A7E630    | 500 GB | 1       | 535   | 0     | 1.47   |
| WDC       | WD3200AAKS-00V6A0  | 320 GB | 1       | 533   | 0     | 1.46   |
| WDC       | WD80EZAZ-11TDBA0   | 8 TB   | 5       | 528   | 0     | 1.45   |
| IBM       | DBCA-204860        | 4 GB   | 1       | 522   | 0     | 1.43   |
| Hitachi   | HTS541660J9SA00    | 64 GB  | 1       | 517   | 0     | 1.42   |
| WDC       | WD100EMAZ-00WJTA0  | 10 TB  | 1       | 517   | 0     | 1.42   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 1       | 508   | 0     | 1.39   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 2       | 507   | 0     | 1.39   |
| HGST      | HTS721010A9E630    | 1 TB   | 3       | 499   | 0     | 1.37   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 5       | 475   | 0     | 1.30   |
| Seagate   | ST1000LX015-1U7172 | 1 TB   | 1       | 467   | 0     | 1.28   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 3       | 1490  | 3     | 1.27   |
| HGST      | HDN726040ALE614    | 4 TB   | 1       | 461   | 0     | 1.26   |
| Seagate   | ST3250410AS        | 250 GB | 1       | 458   | 0     | 1.26   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 1       | 455   | 0     | 1.25   |
| WDC       | WD6400AAKS-22A7B2  | 640 GB | 1       | 446   | 0     | 1.22   |
| WDC       | WD5000BPVT-24HXZT3 | 500 GB | 1       | 429   | 0     | 1.18   |
| WDC       | WD5000AAKS-00A7B0  | 500 GB | 1       | 424   | 0     | 1.16   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 5       | 537   | 7     | 1.16   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 1       | 422   | 0     | 1.16   |
| Toshiba   | HDWQ140            | 4 TB   | 4       | 410   | 0     | 1.12   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 1       | 409   | 0     | 1.12   |
| HGST      | HUS722T2TALA604    | 2 TB   | 4       | 544   | 4     | 1.11   |
| Hitachi   | HTS547550A9E384    | 500 GB | 3       | 681   | 49    | 1.10   |
| Hitachi   | HTS723220L9A360    | 200 GB | 1       | 401   | 0     | 1.10   |
| Toshiba   | HDWD120            | 2 TB   | 2       | 400   | 0     | 1.10   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 2       | 790   | 832   | 1.08   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 4       | 393   | 0     | 1.08   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 5       | 474   | 2     | 1.08   |
| Hitachi   | HDT725032VLA380    | 320 GB | 1       | 389   | 0     | 1.07   |
| WDC       | WD7500BPVT-80HXZT3 | 752 GB | 1       | 389   | 0     | 1.07   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 4       | 388   | 0     | 1.06   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 1       | 1545  | 3     | 1.06   |
| Seagate   | ST380811AS         | 80 GB  | 1       | 383   | 0     | 1.05   |
| HGST      | HUS726020ALA610    | 2 TB   | 1       | 381   | 0     | 1.04   |
| Toshiba   | MK1517GAP          | 16 GB  | 1       | 380   | 0     | 1.04   |
| Seagate   | ST31500541AS       | 1.5 TB | 5       | 649   | 119   | 1.03   |
| HPE       | MB4000GCWLV        | 4 TB   | 4       | 366   | 0     | 1.00   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 8       | 465   | 15    | 0.98   |
| WDC       | WD5000LPVX-60V0TT0 | 500 GB | 1       | 341   | 0     | 0.94   |
| Seagate   | ST2000NE0025-2F... | 2 TB   | 2       | 338   | 0     | 0.93   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 1       | 334   | 0     | 0.92   |
| WDC       | WD2500BEVT-22A23T0 | 250 GB | 2       | 330   | 0     | 0.91   |
| Samsung   | HM160HI            | 160 GB | 1       | 989   | 2     | 0.90   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 4       | 328   | 0     | 0.90   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 1       | 328   | 0     | 0.90   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 5       | 328   | 0     | 0.90   |
| Toshiba   | MK3259GSXP         | 320 GB | 1       | 326   | 0     | 0.89   |
| WDC       | WD120EMAZ-11BLFA0  | 12 TB  | 1       | 323   | 0     | 0.89   |
| WDC       | WD20NMVW-59EDZS7   | 2 TB   | 1       | 320   | 0     | 0.88   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 3       | 678   | 24    | 0.88   |
| WDC       | WD3200BEKT-75PVMT1 | 320 GB | 1       | 315   | 0     | 0.87   |
| WDC       | WD80EZZX-11CSGA0   | 8 TB   | 4       | 387   | 2     | 0.85   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 4       | 280   | 0     | 0.77   |
| WDC       | WD2002FYPS-01U1B0  | 2 TB   | 2       | 1571  | 6     | 0.77   |
| Apple     | HDD HTS545050A7... | 500 GB | 1       | 278   | 0     | 0.76   |
| WDC       | WD3200BEVT-22ZCT0  | 320 GB | 1       | 276   | 0     | 0.76   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 4       | 267   | 0     | 0.73   |
| HGST      | HTS725050A7E630    | 500 GB | 4       | 659   | 256   | 0.72   |
| Seagate   | ST3750640NS        | 752 GB | 2       | 2066  | 1043  | 0.71   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 4       | 255   | 0     | 0.70   |
| Seagate   | ST3120211AS        | 120 GB | 1       | 508   | 1     | 0.70   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 1       | 2015  | 7     | 0.69   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 1       | 248   | 0     | 0.68   |
| WDC       | WD20SDZW-11JJ8S0   | 2 TB   | 1       | 244   | 0     | 0.67   |
| Seagate   | ST380215A          | 80 GB  | 1       | 242   | 0     | 0.66   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 2       | 234   | 0     | 0.64   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 2       | 233   | 0     | 0.64   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 1       | 230   | 0     | 0.63   |
| HGST      | HTS541075A7E630    | 752 GB | 2       | 321   | 507   | 0.62   |
| Hitachi   | HTE723225A7A364    | 250 GB | 1       | 227   | 0     | 0.62   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 1       | 678   | 2     | 0.62   |
| Hitachi   | HTS543232L9A300    | 320 GB | 1       | 223   | 0     | 0.61   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 2       | 220   | 0     | 0.60   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 1       | 652   | 2     | 0.60   |
| HGST      | HUH721010ALE604    | 10 TB  | 1       | 204   | 0     | 0.56   |
| Samsung   | HD502HI            | 500 GB | 1       | 204   | 0     | 0.56   |
| Fujitsu   | MHZ2320BH FFS G1   | 320 GB | 1       | 203   | 0     | 0.56   |
| Toshiba   | HDWD110            | 1 TB   | 8       | 202   | 0     | 0.55   |
| Hitachi   | HDS5C3030ALA630    | 3 TB   | 5       | 247   | 5     | 0.55   |
| WDC       | WD10SPZX-22Z10T0   | 1 TB   | 1       | 197   | 0     | 0.54   |
| Seagate   | ST500LM012 HN-M... | 500 GB | 2       | 193   | 0     | 0.53   |
| Toshiba   | MQ01ABD100         | 1 TB   | 5       | 286   | 143   | 0.52   |
| ExcelStor | J8160S             | 160 GB | 2       | 1003  | 15    | 0.51   |
| Seagate   | ST2000DL004 HD2... | 2 TB   | 1       | 180   | 0     | 0.49   |
| WDC       | WD7500BPKX-80HPJT0 | 752 GB | 1       | 178   | 0     | 0.49   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 6       | 216   | 152   | 0.47   |
| Seagate   | ST3500320NS        | 500 GB | 1       | 1324  | 7     | 0.45   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 1       | 164   | 0     | 0.45   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 1       | 163   | 0     | 0.45   |
| WDC       | WD800BB-00HEA0     | 80 GB  | 1       | 4322  | 26    | 0.44   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 1       | 1390  | 8     | 0.42   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 1       | 153   | 0     | 0.42   |
| Maxtor    | STM3250310AS       | 250 GB | 1       | 140   | 0     | 0.39   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 3       | 332   | 2     | 0.37   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 3       | 134   | 0     | 0.37   |
| Hitachi   | HTS543225L9A300    | 250 GB | 1       | 736   | 5     | 0.34   |
| WDC       | WD10EURX-83UY4Y0   | 1 TB   | 1       | 121   | 0     | 0.33   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 8       | 134   | 1     | 0.33   |
| Seagate   | ST3120026A         | 120 GB | 1       | 1076  | 8     | 0.33   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 4       | 115   | 0     | 0.32   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 3       | 114   | 0     | 0.31   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 1       | 571   | 4     | 0.31   |
| Seagate   | ST9120822AS        | 120 GB | 1       | 1028  | 8     | 0.31   |
| Seagate   | ST9500530NS 42D... | 500 GB | 2       | 221   | 48    | 0.31   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 1       | 111   | 0     | 0.31   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 2       | 277   | 4     | 0.30   |
| Toshiba   | MQ01ABF050         | 500 GB | 3       | 195   | 1     | 0.29   |
| WDC       | WD3200BEVT-00A0RT0 | 320 GB | 1       | 946   | 8     | 0.29   |
| Hitachi   | HTS421260H9AT00    | 64 GB  | 1       | 1338  | 12    | 0.28   |
| Seagate   | ST3000VN007-2E4166 | 3 TB   | 2       | 101   | 0     | 0.28   |
| Toshiba   | MK7575GSX          | 752 GB | 1       | 604   | 5     | 0.28   |
| Toshiba   | HDWN180            | 8 TB   | 3       | 87    | 0     | 0.24   |
| HGST      | HTS545050A7E680    | 500 GB | 1       | 86    | 0     | 0.24   |
| HGST      | HUS724040ALA640    | 4 TB   | 2       | 85    | 0     | 0.23   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 1       | 82    | 0     | 0.23   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 2       | 163   | 1     | 0.22   |
| WDC       | WD60EZRZ-22GZ5B1   | 6 TB   | 1       | 81    | 0     | 0.22   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 1       | 243   | 2     | 0.22   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 1       | 2216  | 28    | 0.21   |
| WDC       | WD2500HHTZ-04N21V1 | 250 GB | 1       | 74    | 0     | 0.20   |
| Toshiba   | MQ04ABF100         | 1 TB   | 6       | 85    | 1     | 0.18   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 3       | 118   | 48    | 0.18   |
| WDC       | WD120EFAX-68UNTN0  | 12 TB  | 1       | 59    | 0     | 0.16   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 1       | 56    | 0     | 0.15   |
| Seagate   | ST500LM030-2E717D  | 500 GB | 1       | 55    | 0     | 0.15   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 1       | 52    | 0     | 0.14   |
| Hitachi   | HTS543232L9SA02    | 320 GB | 1       | 1954  | 37    | 0.14   |
| Hitachi   | HTS543232A7A384    | 320 GB | 2       | 198   | 512   | 0.14   |
| Seagate   | ST3250820AS        | 250 GB | 1       | 392   | 7     | 0.13   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 2       | 48    | 0     | 0.13   |
| WDC       | WD1600BEVT-22ZCT0  | 160 GB | 1       | 45    | 0     | 0.13   |
| Hitachi   | HTS725025A9A364    | 250 GB | 1       | 548   | 11    | 0.13   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 1       | 41    | 0     | 0.11   |
| WDC       | WD5000LPCX-21VHAT0 | 500 GB | 1       | 39    | 0     | 0.11   |
| Hitachi   | HTS541060G9SA00    | 64 GB  | 1       | 255   | 6     | 0.10   |
| Fujitsu   | MHS2040AT D        | 40 GB  | 1       | 1334  | 37    | 0.10   |
| Seagate   | ST500LM021-1KJ152  | 500 GB | 3       | 342   | 710   | 0.09   |
| WDC       | WD10EURX-61C57Y0   | 1 TB   | 1       | 33    | 0     | 0.09   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 1       | 31    | 0     | 0.09   |
| Hitachi   | HDP725050GLA360    | 500 GB | 1       | 1174  | 38    | 0.08   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 1       | 29    | 0     | 0.08   |
| Toshiba   | MG04ACA600E        | 6 TB   | 1       | 28    | 0     | 0.08   |
| Hitachi   | HTS541680J9SA00    | 80 GB  | 1       | 977   | 36    | 0.07   |
| Samsung   | HM320JI            | 320 GB | 1       | 258   | 9     | 0.07   |
| Toshiba   | DT01ABA300         | 3 TB   | 1       | 232   | 8     | 0.07   |
| WDC       | WD10SDZW-11UMGS0   | 1 TB   | 1       | 24    | 0     | 0.07   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 1       | 22    | 0     | 0.06   |
| WDC       | WD20SPZX-22UA7T0   | 2 TB   | 2       | 22    | 0     | 0.06   |
| WDC       | WD3200BEVE-00A0HT0 | 320 GB | 1       | 20    | 0     | 0.05   |
| Seagate   | ST95005620AS       | 500 GB | 1       | 360   | 19    | 0.05   |
| Seagate   | ST31000528AS       | 1 TB   | 1       | 17    | 0     | 0.05   |
| Seagate   | ST9250827AS        | 250 GB | 1       | 564   | 31    | 0.05   |
| Seagate   | ST9500325AS        | 500 GB | 1       | 2276  | 128   | 0.05   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 1       | 16    | 0     | 0.04   |
| Toshiba   | MK5061GSYN         | 500 GB | 1       | 15    | 0     | 0.04   |
| WDC       | WD120EMFZ-11A6JA0  | 12 TB  | 1       | 13    | 0     | 0.04   |
| HGST      | HUS726040ALA610    | 4 TB   | 1       | 1058  | 78    | 0.04   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 6       | 12    | 0     | 0.03   |
| WDC       | WD10SPZX-24Z10     | 1 TB   | 2       | 56    | 3     | 0.03   |
| Samsung   | HM080HI            | 80 GB  | 1       | 627   | 56    | 0.03   |
| Toshiba   | MK3265GSXN         | 320 GB | 1       | 113   | 10    | 0.03   |
| Seagate   | ST31500341AS       | 1.5 TB | 1       | 36    | 3     | 0.03   |
| Toshiba   | MQ03UBB300         | 3 TB   | 1       | 8     | 0     | 0.02   |
| Hitachi   | HTS543212L9A300    | 120 GB | 2       | 1802  | 550   | 0.02   |
| Hitachi   | HDP725016GLA380    | 160 GB | 1       | 1804  | 250   | 0.02   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 1       | 1511  | 220   | 0.02   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 1       | 2670  | 395   | 0.02   |
| WDC       | WD2500BEVT-60A23T0 | 250 GB | 1       | 250   | 37    | 0.02   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 1       | 450   | 78    | 0.02   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 4       | 5     | 0     | 0.02   |
| Toshiba   | MK8025GAS          | 80 GB  | 1       | 5     | 0     | 0.01   |
| Toshiba   | MQ02ABD100H        | 1 TB   | 1       | 349   | 69    | 0.01   |
| Samsung   | HM500JI            | 500 GB | 1       | 1050  | 210   | 0.01   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 1       | 100   | 21    | 0.01   |
| WDC       | WD3200BEVT-60ZCT0  | 320 GB | 1       | 133   | 29    | 0.01   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3160815A         | 160 GB | 1       | 4054  | 1048  | 0.01   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 16      | 3     | 0     | 0.01   |
| WDC       | WD5000AAKS-60WWPA0 | 500 GB | 1       | 798   | 241   | 0.01   |
| Maxtor    | 6Y080P0            | 82 GB  | 2       | 9     | 7     | 0.01   |
| Toshiba   | MK2018GAP          | 20 GB  | 1       | 126   | 55    | 0.01   |
| HGST      | HTS725025A7E630    | 250 GB | 1       | 43    | 20    | 0.01   |
| Seagate   | ST3500514NS        | 500 GB | 1       | 205   | 103   | 0.01   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 1       | 1     | 0     | 0.00   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 1       | 1     | 0     | 0.00   |
| Seagate   | ST9500420AS        | 500 GB | 3       | 810   | 1095  | 0.00   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 2       | 555   | 1009  | 0.00   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 3       | 485   | 1010  | 0.00   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 1       | 165   | 372   | 0.00   |
| Hitachi   | HTS725032A7E630    | 320 GB | 1       | 348   | 1025  | 0.00   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 1       | 234   | 760   | 0.00   |
| Hitachi   | HTS545050A7E380    | 500 GB | 1       | 93    | 345   | 0.00   |
| WDC       | WD5000B            | 500 GB | 1       | 252   | 1011  | 0.00   |
| Hitachi   | DK23AA-12          | 12 GB  | 1       | 4     | 31    | 0.00   |
| Hitachi   | HTS545032B9A300    | 320 GB | 1       | 103   | 1024  | 0.00   |
| HGST      | HTS541010A7E630    | 1 TB   | 1       | 96    | 1023  | 0.00   |
| Seagate   | ST3320418AS        | 320 GB | 1       | 35    | 1086  | 0.00   |
| Maxtor    | 6E040L0            | 41 GB  | 1       | 20    | 1133  | 0.00   |
| Samsung   | HM250JI            | 250 GB | 1       | 16    | 1010  | 0.00   |
| Toshiba   | MK1059GSM          | 1 TB   | 1       | 8     | 558   | 0.00   |
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
| Hitachi   | Deskstar 7K500         | 1      | 1       | 3763  | 0     | 10.31  |
| Hitachi   | Deskstar 7K1000.B      | 2      | 2       | 3658  | 0     | 10.02  |
| WDC       | RE3                    | 1      | 3       | 3329  | 0     | 9.12   |
| WDC       | Caviar SE              | 3      | 7       | 3960  | 3     | 8.90   |
| Hitachi   | Sun Internal           | 1      | 2       | 2785  | 0     | 7.63   |
| Seagate   | Constellation ES.2 ... | 1      | 1       | 2713  | 0     | 7.43   |
| Hitachi   | Travelstar 5K250       | 1      | 1       | 2643  | 0     | 7.24   |
| WDC       | RE4                    | 3      | 8       | 2643  | 0     | 7.24   |
| Hitachi   | Deskstar 7K160         | 1      | 1       | 2187  | 0     | 5.99   |
| WDC       | Caviar Green           | 6      | 11      | 2799  | 240   | 5.79   |
| Hitachi   | Ultrastar A7K2000      | 2      | 6       | 2385  | 61    | 5.74   |
| Hitachi   | Deskstar 7K80          | 1      | 1       | 2086  | 0     | 5.72   |
| Samsung   | SpinPoint F3           | 2      | 4       | 2482  | 1     | 5.67   |
| Hitachi   | Ultrastar 7K3000       | 3      | 10      | 2027  | 0     | 5.55   |
| Toshiba   | 2.5" HDD MQ01ABD..H    | 1      | 1       | 1970  | 0     | 5.40   |
| WDC       | Caviar Black           | 13     | 25      | 2320  | 18    | 5.21   |
| WDC       | Green                  | 10     | 24      | 1903  | 0     | 5.21   |
| Samsung   | SpinPoint F4 EG (AF)   | 1      | 3       | 1849  | 0     | 5.07   |
| HGST      | Ultrastar He8          | 1      | 1       | 1820  | 0     | 4.99   |
| Samsung   | SpinPoint T166         | 1      | 5       | 3372  | 2     | 4.87   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 1      | 5       | 1631  | 0     | 4.47   |
| Seagate   | Constellation.2 (SATA) | 1      | 1       | 1630  | 0     | 4.47   |
| Seagate   | Constellation ES.3     | 3      | 6       | 1627  | 0     | 4.46   |
| WDC       | RE                     | 3      | 8       | 1714  | 1     | 4.30   |
| WDC       | Caviar Blue            | 9      | 9       | 1654  | 27    | 4.29   |
| Seagate   | Barracuda ES           | 3      | 6       | 2392  | 348   | 4.27   |
| Seagate   | Barracuda XT           | 1      | 1       | 1539  | 0     | 4.22   |
| Hitachi   | Deskstar T7K500        | 2      | 2       | 1535  | 0     | 4.21   |
| WDC       | Caviar                 | 2      | 2       | 3565  | 13    | 4.07   |
| Seagate   | Constellation CS       | 2      | 5       | 1808  | 23    | 3.98   |
| Seagate   | Enterprise Capacity... | 1      | 1       | 1376  | 0     | 3.77   |
| HGST      | Ultrastar 7K4000       | 2      | 6       | 1350  | 0     | 3.70   |
| Seagate   | Archive HDD            | 1      | 3       | 1348  | 0     | 3.69   |
| Samsung   | SpinPoint F1 DT        | 2      | 6       | 2114  | 27    | 3.65   |
| Hitachi   | Deskstar 7K1000        | 1      | 1       | 3610  | 2     | 3.30   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 25      | 1289  | 42    | 3.23   |
| WDC       | Unknown                | 1      | 1       | 1179  | 0     | 3.23   |
| Seagate   | Desktop HDD.15         | 3      | 9       | 1171  | 0     | 3.21   |
| Samsung   | SpinPoint P120         | 1      | 1       | 1158  | 0     | 3.17   |
| HGST      | Deskstar NAS           | 4      | 12      | 1501  | 67    | 3.14   |
| Seagate   | Barracuda 7200.12      | 8      | 19      | 1267  | 58    | 3.04   |
| Seagate   | Video 2.5              | 1      | 1       | 1083  | 0     | 2.97   |
| Toshiba   | 2.5" HDD MQ01UBB       | 1      | 1       | 1067  | 0     | 2.93   |
| Toshiba   | 3.5" MG04ACA Enterp... | 2      | 3       | 1033  | 0     | 2.83   |
| Toshiba   | X300                   | 1      | 6       | 1186  | 5     | 2.73   |
| WDC       | Red                    | 18     | 143     | 1136  | 10    | 2.71   |
| WDC       | VelociRaptor           | 2      | 2       | 949   | 0     | 2.60   |
| Seagate   | Barracuda Green (AF)   | 1      | 7       | 1631  | 174   | 2.57   |
| Hitachi   | Deskstar 7K3000        | 2      | 2       | 918   | 0     | 2.52   |
| Toshiba   | 2.5" HDD MQ04UBD       | 1      | 1       | 906   | 0     | 2.48   |
| HGST      | Travelstar 5K1000      | 1      | 3       | 869   | 0     | 2.38   |
| Seagate   | Skyhawk                | 1      | 2       | 861   | 0     | 2.36   |
| Seagate   | U6                     | 1      | 1       | 2579  | 2     | 2.36   |
| Seagate   | Surveillance           | 2      | 2       | 851   | 0     | 2.33   |
| Seagate   | Barracuda 7200.14 (AF) | 12     | 34      | 1014  | 128   | 2.32   |
| WDC       | Elements / My Passport | 6      | 6       | 810   | 0     | 2.22   |
| WDC       | Purple                 | 4      | 5       | 810   | 0     | 2.22   |
| Toshiba   | Unknown                | 2      | 3       | 809   | 0     | 2.22   |
| Seagate   | Barracuda 7200.7 an... | 4      | 4       | 1518  | 3     | 2.16   |
| Seagate   | Pipeline HD 5900.2     | 2      | 3       | 736   | 0     | 2.02   |
| WDC       | Blue                   | 36     | 62      | 761   | 1     | 1.97   |
| Seagate   | Exos X12               | 1      | 1       | 710   | 0     | 1.95   |
| Seagate   | SpinPoint M8 (AF)      | 3      | 10      | 774   | 2     | 1.93   |
| Seagate   | Constellation ES (S... | 1      | 1       | 2080  | 2     | 1.90   |
| Fujitsu   | MJA BH                 | 2      | 2       | 670   | 0     | 1.84   |
| WDC       | Ultrastar He10/12      | 2      | 12      | 661   | 0     | 1.81   |
| Seagate   | Barracuda 7200.10      | 7      | 8       | 1248  | 154   | 1.81   |
| Seagate   | IronWolf Pro           | 2      | 4       | 649   | 0     | 1.78   |
| Samsung   | SpinPoint F2 EG        | 2      | 3       | 1565  | 50    | 1.66   |
| ExcelStor | Jupiter                | 2      | 4       | 1009  | 8     | 1.64   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 1       | 592   | 0     | 1.62   |
| WDC       | Red Pro                | 5      | 7       | 576   | 0     | 1.58   |
| Seagate   | NAS HDD                | 2      | 4       | 569   | 0     | 1.56   |
| Seagate   | Barracuda LP           | 2      | 6       | 791   | 99    | 1.54   |
| Samsung   | SpinPoint P80 SD       | 1      | 1       | 547   | 0     | 1.50   |
| WDC       | HGST Ultrastar He10    | 2      | 6       | 526   | 0     | 1.44   |
| Hitachi   | Travelstar 7K320       | 2      | 2       | 523   | 0     | 1.43   |
| IBM       | Travelstar 6GN         | 1      | 1       | 522   | 0     | 1.43   |
| Hitachi   | Deskstar 7K1000.C      | 3      | 3       | 1171  | 74    | 1.42   |
| Hitachi   | Travelstar 5K500.B     | 2      | 2       | 555   | 512   | 1.38   |
| HGST      | Travelstar 7K1000      | 1      | 3       | 499   | 0     | 1.37   |
| Seagate   | Barracuda 2.5 5400     | 5      | 21      | 473   | 0     | 1.30   |
| Seagate   | FireCuda 2.5           | 1      | 1       | 467   | 0     | 1.28   |
| WDC       | RE2                    | 1      | 1       | 455   | 0     | 1.25   |
| Toshiba   | 3.5" HDD N300          | 1      | 4       | 410   | 0     | 1.12   |
| Seagate   | Momentus 5400.6        | 2      | 3       | 1377  | 380   | 1.11   |
| HGST      | Ultrastar 7K2          | 1      | 4       | 544   | 4     | 1.11   |
| Hitachi   | Travelstar 5K750       | 1      | 3       | 681   | 49    | 1.10   |
| Seagate   | Barracuda 3.5          | 5      | 17      | 505   | 11    | 1.07   |
| Seagate   | BarraCuda 3.5          | 2      | 8       | 403   | 18    | 1.05   |
| HPE       | Proliant HardDrive     | 1      | 4       | 366   | 0     | 1.00   |
| Toshiba   | P300                   | 3      | 14      | 360   | 0     | 0.99   |
| WDC       | Scorpio Blue           | 13     | 14      | 438   | 6     | 0.96   |
| Seagate   | Momentus 7200.4        | 2      | 4       | 958   | 821   | 0.96   |
| WDC       | Black                  | 3      | 8       | 353   | 1     | 0.91   |
| Toshiba   | 2.5" HDD MK..59GSXP    | 1      | 1       | 326   | 0     | 0.89   |
| Seagate   | Barracuda Compute      | 2      | 5       | 320   | 0     | 0.88   |
| Seagate   | Barracuda 7200.9       | 2      | 2       | 446   | 1     | 0.87   |
| WDC       | RE4-GP                 | 1      | 2       | 1571  | 6     | 0.77   |
| Apple     | HGST Travelstar Z5K500 | 1      | 1       | 278   | 0     | 0.76   |
| Hitachi   | Travelstar 5K160       | 2      | 2       | 747   | 18    | 0.75   |
| Hitachi   | Travelstar Z7K500      | 2      | 2       | 442   | 513   | 0.73   |
| HGST      | Ultrastar DC HC320     | 1      | 2       | 233   | 0     | 0.64   |
| WDC       | Blue Mobile            | 4      | 5       | 279   | 203   | 0.63   |
| Hitachi   | Travelstar Z7K320      | 1      | 1       | 227   | 0     | 0.62   |
| HGST      | Travelstar Z7K500      | 2      | 5       | 536   | 209   | 0.58   |
| HGST      | Ultrastar He10         | 1      | 1       | 204   | 0     | 0.56   |
| Fujitsu   | MHZ BH                 | 1      | 1       | 203   | 0     | 0.56   |
| Hitachi   | Ultrastar 7K4000       | 2      | 13      | 208   | 1     | 0.55   |
| Hitachi   | Deskstar 5K3000        | 1      | 5       | 247   | 5     | 0.55   |
| HGST      | Ultrastar 7K6000       | 2      | 2       | 720   | 39    | 0.54   |
| Hitachi   | Travelstar 7K100       | 2      | 2       | 772   | 20    | 0.53   |
| Toshiba   | 2.5" HDD MQ01ABD       | 1      | 5       | 286   | 143   | 0.52   |
| WDC       | Scorpio Black          | 3      | 3       | 333   | 1     | 0.52   |
| Seagate   | SpinPoint F4 EG (AF)   | 1      | 1       | 180   | 0     | 0.49   |
| Seagate   | Laptop HDD             | 4      | 8       | 484   | 645   | 0.46   |
| Seagate   | Barracuda ES.2         | 1      | 1       | 1324  | 7     | 0.45   |
| Samsung   | SpinPoint M5           | 2      | 2       | 502   | 506   | 0.45   |
| Seagate   | Mobile HDD             | 2      | 7       | 201   | 130   | 0.44   |
| HGST      | Travelstar Z5K1000     | 2      | 3       | 246   | 679   | 0.42   |
| WDC       | Black Mobile           | 5      | 7       | 233   | 1     | 0.41   |
| Seagate   | IronWolf               | 7      | 33      | 143   | 0     | 0.39   |
| Maxtor    | DiamondMax 21          | 1      | 1       | 140   | 0     | 0.39   |
| Seagate   | Momentus 5400.3        | 1      | 1       | 1028  | 8     | 0.31   |
| Seagate   | Constellation          | 1      | 2       | 221   | 48    | 0.31   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 3       | 195   | 1     | 0.29   |
| Hitachi   | Travelstar 4K120       | 1      | 1       | 1338  | 12    | 0.28   |
| Toshiba   | 2.5" HDD MK..75GSX     | 1      | 1       | 604   | 5     | 0.28   |
| Toshiba   | N300                   | 1      | 3       | 87    | 0     | 0.24   |
| HGST      | Travelstar Z5K500      | 1      | 1       | 86    | 0     | 0.24   |
| Hitachi   | Travelstar 5K320       | 4      | 5       | 1304  | 229   | 0.23   |
| WDC       | Internal Use HDD       | 1      | 1       | 82    | 0     | 0.23   |
| WDC       | AV-GP                  | 2      | 2       | 77    | 0     | 0.21   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 6       | 85    | 1     | 0.18   |
| Hitachi   | Ultrastar A7K1000      | 1      | 1       | 52    | 0     | 0.14   |
| Hitachi   | Travelstar Z5K320      | 1      | 2       | 198   | 512   | 0.14   |
| Hitachi   | Travelstar 7K500       | 1      | 1       | 548   | 11    | 0.13   |
| Hitachi   | Travelstar 5K100       | 1      | 1       | 255   | 6     | 0.10   |
| Fujitsu   | MHS AT                 | 1      | 1       | 1334  | 37    | 0.10   |
| Samsung   | SpinPoint M6           | 1      | 1       | 258   | 9     | 0.07   |
| Toshiba   | 3.5" DT01ABA Deskto... | 1      | 1       | 232   | 8     | 0.07   |
| WDC       | Scorpio Blue EIDE      | 1      | 1       | 20    | 0     | 0.05   |
| Hitachi   | Deskstar P7K500        | 2      | 2       | 1489  | 144   | 0.05   |
| Seagate   | Momentus XT            | 1      | 1       | 360   | 19    | 0.05   |
| Seagate   | Momentus 5400.4        | 1      | 1       | 564   | 31    | 0.05   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 1      | 1       | 15    | 0     | 0.04   |
| Samsung   | SpinPoint M40/60/80    | 1      | 1       | 627   | 56    | 0.03   |
| Toshiba   | 2.5" HDD MK..65GSX     | 1      | 1       | 113   | 10    | 0.03   |
| Seagate   | Barracuda 7200.11      | 1      | 1       | 36    | 3     | 0.03   |
| Toshiba   | 2.5" HDD MQ03UBB       | 1      | 1       | 8     | 0     | 0.02   |
| Toshiba   | 2.5" HDD MQ02ABD..H    | 1      | 1       | 349   | 69    | 0.01   |
| Samsung   | SpinPoint M7           | 1      | 1       | 1050  | 210   | 0.01   |
| Toshiba   | 2.5" HDD               | 2      | 2       | 65    | 28    | 0.01   |
| Maxtor    | DiamondMax Plus 9      | 1      | 2       | 9     | 7     | 0.01   |
| Seagate   | Constellation ES (S... | 1      | 1       | 205   | 103   | 0.01   |
| Seagate   | Momentus Thin          | 1      | 2       | 555   | 1009  | 0.00   |
| WDC       | Gold                   | 1      | 1       | 165   | 372   | 0.00   |
| Hitachi   | Travelstar Z5K500      | 1      | 1       | 93    | 345   | 0.00   |
| Hitachi   | Travelstar DK23XX/D... | 1      | 1       | 4     | 31    | 0.00   |
| Maxtor    | DiamondMax Plus 8      | 1      | 1       | 20    | 1133  | 0.00   |
| Toshiba   | 2.5" HDD MK..59GSM     | 1      | 1       | 8     | 558   | 0.00   |

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
| Samsung     | 15     | 28      | 1942  | 58    | 3.39   |
| WDC         | 161    | 386     | 1251  | 17    | 3.01   |
| Hitachi     | 48     | 79      | 1198  | 73    | 2.55   |
| HGST        | 19     | 43      | 926   | 93    | 2.04   |
| Toshiba     | 32     | 91      | 756   | 28    | 1.89   |
| Seagate     | 110    | 261     | 857   | 92    | 1.84   |
| ExcelStor   | 2      | 4       | 1009  | 8     | 1.64   |
| IBM         | 1      | 1       | 522   | 0     | 1.43   |
| Fujitsu     | 4      | 4       | 719   | 10    | 1.08   |
| HPE         | 1      | 4       | 366   | 0     | 1.00   |
| Apple       | 1      | 1       | 278   | 0     | 0.76   |
| Maxtor      | 3      | 4       | 45    | 287   | 0.10   |

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
| Samsung   | SSD 840 EVO        | 120 GB | 2       | 3427  | 0     | 9.39   |
| Intel     | SSDSA2M040G2GC     | 40 GB  | 1       | 2739  | 0     | 7.51   |
| WDC       | WDBNCE5000PNC      | 500 GB | 1       | 2730  | 0     | 7.48   |
| Samsung   | SSD 840 Series     | 120 GB | 1       | 2655  | 0     | 7.28   |
| Samsung   | SSD 840 PRO Series | 128 GB | 1       | 2487  | 0     | 6.81   |
| OCZ       | AGILITY3           | 120 GB | 1       | 2119  | 0     | 5.81   |
| Samsung   | MZ7TD256HAFV-000L7 | 256 GB | 1       | 2052  | 0     | 5.62   |
| Intel     | SSDSC2CT180A3      | 180 GB | 2       | 2012  | 0     | 5.51   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 1       | 1964  | 0     | 5.38   |
| Intel     | SSDSC2BF120A5      | 120 GB | 1       | 1960  | 0     | 5.37   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 2       | 1958  | 0     | 5.37   |
| OCZ       | VERTEX3            | 64 GB  | 2       | 1948  | 0     | 5.34   |
| ADATA     | SP310              | 32 GB  | 1       | 1944  | 0     | 5.33   |
| Samsung   | SSD PB22-JS3 TM    | 64 GB  | 1       | 1801  | 0     | 4.94   |
| Samsung   | SSD 850 PRO        | 128 GB | 2       | 1798  | 0     | 4.93   |
| Kingston  | SH103S3240G        | 240 GB | 1       | 1798  | 0     | 4.93   |
| Kingston  | SMS200S360G        | 64 GB  | 2       | 1773  | 0     | 4.86   |
| OCZ       | VERTEX3            | 120 GB | 1       | 1657  | 0     | 4.54   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 1       | 1656  | 0     | 4.54   |
| Samsung   | MZMTE512HMHP-000MV | 512 GB | 2       | 1593  | 0     | 4.36   |
| ADATA     | SP900              | 128 GB | 1       | 1548  | 0     | 4.24   |
| SK hynix  | HFS256G3AMNB-2200A | 256 GB | 1       | 1542  | 0     | 4.22   |
| Goodram   | SSD                | 240 GB | 2       | 1509  | 0     | 4.13   |
| ADATA     | SP310              | 128 GB | 1       | 1488  | 0     | 4.08   |
| SanDisk   | SSD U100           | 16 GB  | 1       | 1440  | 0     | 3.95   |
| Intel     | SSDSC2BW240A3L     | 240 GB | 1       | 1425  | 0     | 3.91   |
| Samsung   | SSD 750 EVO        | 120 GB | 1       | 1425  | 0     | 3.91   |
| Samsung   | SSD 840 Series     | 250 GB | 2       | 1328  | 0     | 3.64   |
| Samsung   | MZ7LM240HCGR-0E003 | 240 GB | 2       | 1295  | 0     | 3.55   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 1       | 1219  | 0     | 3.34   |
| SanDisk   | Ultra II           | 960 GB | 2       | 1202  | 0     | 3.29   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 3       | 1191  | 0     | 3.26   |
| Toshiba   | THNSNJ128GCSU      | 128 GB | 2       | 1189  | 0     | 3.26   |
| Samsung   | SSD 840 PRO Series | 256 GB | 2       | 1183  | 0     | 3.24   |
| Samsung   | SSD RBX Series ... | 64 GB  | 1       | 1182  | 0     | 3.24   |
| SuperM... | SSD                | 16 GB  | 1       | 1176  | 0     | 3.22   |
| Samsung   | SSD 850 EVO mSATA  | 1 TB   | 1       | 2157  | 1     | 2.96   |
| SanDisk   | SD7SF6S512G1122    | 512 GB | 1       | 1073  | 0     | 2.94   |
| Transcend | TS64GSSD25S-M      | 64 GB  | 1       | 1067  | 0     | 2.92   |
| Samsung   | MZ7PD128HAFV-000H7 | 128 GB | 1       | 1060  | 0     | 2.91   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 1       | 1060  | 0     | 2.91   |
| Kingston  | SKC400S37512G      | 512 GB | 2       | 1059  | 0     | 2.90   |
| Crucial   | FCCT128M4SSD1      | 128 GB | 2       | 1042  | 0     | 2.86   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 3       | 1033  | 0     | 2.83   |
| ADATA     | SX930              | 240 GB | 1       | 1001  | 0     | 2.74   |
| Crucial   | CT250MX200SSD1     | 250 GB | 5       | 1048  | 1     | 2.68   |
| Kingston  | SH103S3120G        | 120 GB | 2       | 964   | 0     | 2.64   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 1       | 959   | 0     | 2.63   |
| China     | SATA SSD           | 120 GB | 1       | 933   | 0     | 2.56   |
| Crucial   | CT240M500SSD3      | 240 GB | 1       | 917   | 0     | 2.51   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 2       | 898   | 0     | 2.46   |
| Seagate   | ST100FN0021        | 100 GB | 1       | 1781  | 1     | 2.44   |
| SanDisk   | SD8SN8U-256G-1006  | 256 GB | 1       | 888   | 0     | 2.44   |
| Transcend | TS128GSSD370S      | 128 GB | 1       | 868   | 0     | 2.38   |
| Samsung   | SSD 750 EVO        | 500 GB | 1       | 854   | 0     | 2.34   |
| SanDisk   | SD8SN8U128G1122    | 128 GB | 2       | 848   | 0     | 2.33   |
| Corsair   | Force 3 SSD        | 180 GB | 1       | 2530  | 2     | 2.31   |
| OCZ       | VERTEX2            | 120 GB | 1       | 835   | 0     | 2.29   |
| Samsung   | SSD 850 EVO        | 250 GB | 18      | 835   | 0     | 2.29   |
| Intel     | SSDSC2BP240G4      | 240 GB | 1       | 835   | 0     | 2.29   |
| Toshiba   | THNSNC128GBSJ      | 128 GB | 1       | 826   | 0     | 2.26   |
| Kingston  | SUV400S37240G      | 240 GB | 3       | 815   | 0     | 2.23   |
| Kingston  | SUV300S37A240G     | 240 GB | 1       | 807   | 0     | 2.21   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 3       | 804   | 0     | 2.20   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 2       | 798   | 0     | 2.19   |
| SanDisk   | SSD U110           | 16 GB  | 3       | 797   | 0     | 2.19   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 4       | 778   | 0     | 2.13   |
| MyDigi... | SB2                | 128 GB | 1       | 763   | 0     | 2.09   |
| Samsung   | SSD 850 EVO        | 1 TB   | 5       | 1085  | 1     | 2.09   |
| Apple     | SSD TS256C         | 256 GB | 1       | 752   | 0     | 2.06   |
| Samsung   | SSD 850 EVO        | 2 TB   | 1       | 742   | 0     | 2.03   |
| Mushkin   | MKNSSDTR1TB-3DL    | 1 TB   | 1       | 734   | 0     | 2.01   |
| Samsung   | SSD 750 EVO        | 250 GB | 1       | 734   | 0     | 2.01   |
| Samsung   | SSD 840 EVO        | 1 TB   | 1       | 727   | 0     | 1.99   |
| Intel     | SSDSC2BW240H6      | 240 GB | 2       | 723   | 0     | 1.98   |
| Samsung   | MZMPC032HBCD-00000 | 32 GB  | 1       | 721   | 0     | 1.98   |
| Samsung   | SSD 860 EVO        | 2 TB   | 2       | 717   | 0     | 1.97   |
| Samsung   | SSD 840 EVO        | 250 GB | 3       | 690   | 0     | 1.89   |
| Samsung   | MZ7PC128HAFU-000L1 | 128 GB | 1       | 683   | 0     | 1.87   |
| OWC       | Mercury Extreme... | 240 GB | 1       | 657   | 0     | 1.80   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 1       | 651   | 0     | 1.78   |
| Kingston  | SMSM150S324G2      | 24 GB  | 1       | 650   | 0     | 1.78   |
| SanDisk   | Ultra II           | 480 GB | 2       | 622   | 0     | 1.70   |
| SPCC      | SSD                | 1 TB   | 1       | 617   | 0     | 1.69   |
| SanDisk   | SDSSDHII120G       | 120 GB | 1       | 613   | 0     | 1.68   |
| Kingston  | SUV500MS120G       | 120 GB | 3       | 611   | 0     | 1.68   |
| Intel     | SSDSA2CW160G3      | 160 GB | 1       | 610   | 0     | 1.67   |
| SanDisk   | SDSSDXP120G        | 120 GB | 1       | 608   | 0     | 1.67   |
| Samsung   | SSD 850 PRO        | 256 GB | 5       | 608   | 0     | 1.67   |
| Samsung   | MZNLN256HCHP-000L7 | 256 GB | 1       | 595   | 0     | 1.63   |
| Crucial   | M4-CT064M4SSD2     | 64 GB  | 1       | 589   | 0     | 1.61   |
| SanDisk   | SDSSDA120G         | 120 GB | 2       | 566   | 0     | 1.55   |
| Samsung   | SSD 850 EVO        | 500 GB | 10      | 550   | 0     | 1.51   |
| Samsung   | MZ7TE256HMHP-000H1 | 256 GB | 1       | 544   | 0     | 1.49   |
| Phison    | SATA SSD           | 16 GB  | 9       | 533   | 0     | 1.46   |
| Samsung   | MZ7TY256HDHP-000L7 | 256 GB | 1       | 516   | 0     | 1.41   |
| Kingston  | SV300S37A480G      | 480 GB | 1       | 501   | 0     | 1.37   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 3       | 496   | 0     | 1.36   |
| Plextor   | PX-128M7VC         | 128 GB | 1       | 483   | 0     | 1.32   |
| Samsung   | MZ7LN512HMJP-000L7 | 512 GB | 1       | 483   | 0     | 1.32   |
| Patriot   | Burst              | 240 GB | 1       | 467   | 0     | 1.28   |
| AEGO      | SSD                | 120 GB | 1       | 445   | 0     | 1.22   |
| Samsung   | SSD PM830 FDE 2... | 256 GB | 1       | 440   | 0     | 1.21   |
| Vaseky    | V800-60G           | 64 GB  | 1       | 426   | 0     | 1.17   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 2       | 425   | 0     | 1.17   |
| SPCC      | SSD                | 64 GB  | 2       | 424   | 0     | 1.16   |
| SanDisk   | SD8SN8U128G1002    | 128 GB | 1       | 424   | 0     | 1.16   |
| Toshiba   | THNSNJ128GCST      | 128 GB | 1       | 422   | 0     | 1.16   |
| SanDisk   | SDSSDH3512G        | 512 GB | 1       | 415   | 0     | 1.14   |
| Intel     | SSDSC2BB120G4      | 120 GB | 1       | 413   | 0     | 1.13   |
| Transcend | TS512GSSD370       | 512 GB | 1       | 412   | 0     | 1.13   |
| Crucial   | CT525MX300SSD1     | 528 GB | 5       | 512   | 1     | 1.08   |
| Samsung   | SSD PM830 mSATA    | 128 GB | 1       | 385   | 0     | 1.06   |
| Kingston  | SVP200S37A60G      | 64 GB  | 1       | 377   | 0     | 1.03   |
| Hoodisk   | SSD                | 32 GB  | 3       | 372   | 0     | 1.02   |
| Crucial   | CT120M500SSD1      | 120 GB | 2       | 369   | 0     | 1.01   |
| Kingston  | RBUSNS8180S3128GI  | 128 GB | 1       | 351   | 0     | 0.96   |
| Intel     | SSDSC2BB480G7      | 480 GB | 1       | 703   | 1     | 0.96   |
| Samsung   | SSD 860 EVO mSATA  | 1 TB   | 1       | 346   | 0     | 0.95   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 1       | 3057  | 8     | 0.93   |
| Kingston  | SHFS37A120G        | 120 GB | 1       | 334   | 0     | 0.92   |
| Intel     | SSDSA2CW120G3      | 120 GB | 1       | 326   | 0     | 0.89   |
| Samsung   | SSD 860 EVO        | 1 TB   | 6       | 320   | 0     | 0.88   |
| Phison    | SATA SSD           | 128 GB | 1       | 316   | 0     | 0.87   |
| SanDisk   | SSD PLUS           | 120 GB | 8       | 312   | 0     | 0.86   |
| Kingston  | SA400S37240G       | 240 GB | 12      | 308   | 0     | 0.85   |
| Toshiba   | THNSFJ256GCSU      | 256 GB | 2       | 308   | 0     | 0.85   |
| Kingston  | SUV500MS240G       | 240 GB | 4       | 307   | 0     | 0.84   |
| Samsung   | SSD 850 PRO        | 512 GB | 1       | 306   | 0     | 0.84   |
| KingDian  | S400               | 120 GB | 1       | 303   | 0     | 0.83   |
| OCZ       | VERTEX4            | 128 GB | 1       | 1188  | 3     | 0.81   |
| Intel     | SSDSC2CT240A3      | 240 GB | 1       | 2370  | 7     | 0.81   |
| Kingston  | SV300S37A120G      | 120 GB | 4       | 410   | 1     | 0.77   |
| Samsung   | SSD 860 PRO        | 256 GB | 1       | 279   | 0     | 0.76   |
| Kingston  | SMS200S3120G       | 120 GB | 3       | 881   | 3     | 0.76   |
| SanDisk   | SD9SN8W128G1002    | 128 GB | 1       | 278   | 0     | 0.76   |
| Phison    | SATA SSD           | 120 GB | 1       | 273   | 0     | 0.75   |
| Kingston  | SA400S37120G       | 120 GB | 7       | 271   | 0     | 0.74   |
| SanDisk   | SD6SB2M512G1022I   | 512 GB | 1       | 536   | 1     | 0.74   |
| SK hynix  | HFS128G32MND-2200A | 128 GB | 1       | 798   | 2     | 0.73   |
| Intel     | SSDSC2BF180A4L     | 180 GB | 3       | 392   | 2     | 0.72   |
| Samsung   | SSD 850 EVO        | 120 GB | 2       | 255   | 0     | 0.70   |
| SanDisk   | SD5SG2256G1052E    | 256 GB | 1       | 246   | 0     | 0.68   |
| Samsung   | SSD 860 EVO        | 500 GB | 9       | 244   | 0     | 0.67   |
| Intel     | SSDSA2M160G2GC     | 160 GB | 1       | 472   | 1     | 0.65   |
| SK hynix  | HFS128G39TND-N210A | 128 GB | 1       | 232   | 0     | 0.64   |
| Plextor   | PX-256M8VG         | 256 GB | 1       | 230   | 0     | 0.63   |
| SPCC      | SSD                | 120 GB | 1       | 228   | 0     | 0.63   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 1       | 223   | 0     | 0.61   |
| Samsung   | MZHPV512HDGL-000L1 | 512 GB | 1       | 222   | 0     | 0.61   |
| Kingston  | SMS200S330G        | 32 GB  | 2       | 768   | 2     | 0.60   |
| Corsair   | Force LS SSD       | 64 GB  | 2       | 217   | 0     | 0.60   |
| Crucial   | CT275MX300SSD4     | 275 GB | 1       | 213   | 0     | 0.59   |
| OCZ       | VERTEX4            | 64 GB  | 1       | 206   | 0     | 0.57   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 1       | 204   | 0     | 0.56   |
| SanDisk   | X400 M.2 2280      | 512 GB | 1       | 204   | 0     | 0.56   |
| Samsung   | SSD 860 EVO mSATA  | 500 GB | 6       | 203   | 0     | 0.56   |
| Crucial   | CT250MX500SSD1     | 250 GB | 7       | 203   | 0     | 0.56   |
| Crucial   | CT500MX200SSD1     | 500 GB | 2       | 199   | 0     | 0.55   |
| Kingston  | SUV500240G         | 240 GB | 2       | 198   | 0     | 0.55   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 1       | 196   | 0     | 0.54   |
| PNY       | CS900 120GB SSD    | 120 GB | 4       | 189   | 0     | 0.52   |
| Apacer    | 128GB SATA Flas... | 128 GB | 1       | 187   | 0     | 0.51   |
| China     | SSD 128G           | 128 GB | 1       | 181   | 0     | 0.50   |
| Kingston  | SM2280S3G2240G     | 240 GB | 1       | 181   | 0     | 0.50   |
| Hoodisk   | SSD                | 64 GB  | 2       | 180   | 0     | 0.50   |
| KingDian  | S280-240GB         | 240 GB | 1       | 177   | 0     | 0.49   |
| Goodram   | SSD                | 120 GB | 1       | 172   | 0     | 0.47   |
| Apple     | SSD SM0512G        | 500 GB | 1       | 170   | 0     | 0.47   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 2       | 168   | 0     | 0.46   |
| ZTC       | SM201-064G         | 64 GB  | 1       | 164   | 0     | 0.45   |
| Vaseky    | 128GV800           | 128 GB | 1       | 161   | 0     | 0.44   |
| Apacer    | 32GB SATA Flash... | 32 GB  | 1       | 1769  | 10    | 0.44   |
| Samsung   | SSD PM871b M.2 ... | 256 GB | 1       | 158   | 0     | 0.43   |
| China     | 40GB SATA Flash... | 40 GB  | 1       | 156   | 0     | 0.43   |
| SK hynix  | SC311 SATA         | 512 GB | 1       | 153   | 0     | 0.42   |
| Intel     | SSDSCKGF180A4L     | 180 GB | 1       | 152   | 0     | 0.42   |
| Transcend | TS256GSSD230S      | 256 GB | 1       | 147   | 0     | 0.40   |
| Phison    | SATA SSD           | 32 GB  | 1       | 145   | 0     | 0.40   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 1       | 144   | 0     | 0.40   |
| Lite-On   | CV8-8E256-11 SATA  | 256 GB | 1       | 143   | 0     | 0.39   |
| Samsung   | SSD 860 EVO        | 250 GB | 7       | 143   | 0     | 0.39   |
| KingSpec  | NT-128             | 128 GB | 1       | 140   | 0     | 0.38   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 1       | 139   | 0     | 0.38   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 2       | 1461  | 509   | 0.38   |
| Samsung   | SSD 860 QVO        | 4 TB   | 2       | 135   | 0     | 0.37   |
| Toshiba   | TR200              | 240 GB | 2       | 131   | 0     | 0.36   |
| Samsung   | MZHPV256HDGL-000L1 | 256 GB | 1       | 131   | 0     | 0.36   |
| SanDisk   | SD7SN3Q128G1002    | 128 GB | 1       | 131   | 0     | 0.36   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 2       | 130   | 0     | 0.36   |
| WDC       | WDS500G2B0A        | 500 GB | 2       | 125   | 0     | 0.34   |
| Lite-On   | LCS-128M6S-HP      | 128 GB | 1       | 123   | 0     | 0.34   |
| Kingston  | SA400S37480G       | 480 GB | 3       | 119   | 0     | 0.33   |
| SanDisk   | SDSSDH3 512G       | 512 GB | 1       | 116   | 0     | 0.32   |
| Verbatim  | Vi500 S3 480GB SSD | 480 GB | 1       | 115   | 0     | 0.32   |
| Samsung   | SSD 860 QVO        | 1 TB   | 3       | 113   | 0     | 0.31   |
| Crucial   | CT120BX300SSD1     | 120 GB | 1       | 108   | 0     | 0.30   |
| China     | OSSD256GBTSS2      | 256 GB | 1       | 107   | 0     | 0.30   |
| China     | BR                 | 64 GB  | 1       | 106   | 0     | 0.29   |
| Intel     | SSDSC2KG480G8R     | 480 GB | 2       | 105   | 0     | 0.29   |
| Patriot   | Burst              | 120 GB | 1       | 104   | 0     | 0.28   |
| SanDisk   | SD9SN8W128G1102    | 128 GB | 1       | 98    | 0     | 0.27   |
| Apple     | SSD SD0128F        | 121 GB | 1       | 91    | 0     | 0.25   |
| Apple     | SSD SM0128G        | 121 GB | 2       | 91    | 0     | 0.25   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 3       | 89    | 0     | 0.24   |
| Intel     | SSDSC2BW240A4      | 240 GB | 1       | 89    | 0     | 0.24   |
| Samsung   | SSD 860 QVO        | 2 TB   | 1       | 88    | 0     | 0.24   |
| OCZ       | AGILITY4           | 128 GB | 1       | 176   | 1     | 0.24   |
| ADATA     | SU800              | 256 GB | 1       | 85    | 0     | 0.24   |
| ADATA     | SP600              | 64 GB  | 1       | 84    | 0     | 0.23   |
| ADATA     | SU800              | 1 TB   | 1       | 83    | 0     | 0.23   |
| WDC       | WDS120G2G0A-00JH30 | 120 GB | 1       | 82    | 0     | 0.23   |
| KingDian  | S200               | 64 GB  | 2       | 80    | 0     | 0.22   |
| Crucial   | CT500MX500SSD1     | 500 GB | 1       | 77    | 0     | 0.21   |
| Transcend | TS240GMTS420S      | 240 GB | 2       | 77    | 0     | 0.21   |
| Kingston  | SMSM151S3128GD     | 128 GB | 1       | 598   | 7     | 0.21   |
| SPCC      | SSD                | 256 GB | 1       | 71    | 0     | 0.19   |
| Intel     | SSDSC2KG480G8      | 480 GB | 3       | 70    | 0     | 0.19   |
| Samsung   | SSD 860 EVO        | 4 TB   | 1       | 68    | 0     | 0.19   |
| Plextor   | PX-256M5S          | 256 GB | 2       | 64    | 0     | 0.18   |
| WDC       | WDS480G2G0A-00JH30 | 480 GB | 3       | 60    | 0     | 0.16   |
| Samsung   | MZMTE1T0HMJH-00000 | 1 TB   | 1       | 59    | 0     | 0.16   |
| SanDisk   | Ultra II           | 240 GB | 1       | 58    | 0     | 0.16   |
| Kingston  | SUV500MS480G       | 480 GB | 2       | 49    | 0     | 0.14   |
| KingDian  | S280               | 120 GB | 1       | 49    | 0     | 0.14   |
| ADATA     | SU630              | 480 GB | 1       | 48    | 0     | 0.13   |
| Transcend | TS64GMSA370        | 64 GB  | 2       | 47    | 0     | 0.13   |
| Crucial   | CT250MX500SSD4     | 250 GB | 1       | 47    | 0     | 0.13   |
| OCZ       | TRION150           | 240 GB | 1       | 40    | 0     | 0.11   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 8       | 45    | 1     | 0.11   |
| SanDisk   | SD6SB1M256G1022I   | 256 GB | 2       | 1754  | 44    | 0.11   |
| Crucial   | CT120BX500SSD1     | 120 GB | 2       | 39    | 0     | 0.11   |
| WDC       | WDS120G1G0B-00RC30 | 120 GB | 1       | 37    | 0     | 0.10   |
| KingFast  | SSD                | 120 GB | 2       | 37    | 0     | 0.10   |
| SanDisk   | SSD PLUS           | 1 TB   | 1       | 37    | 0     | 0.10   |
| Kingston  | SUV400S37 120G     | 120 GB | 1       | 37    | 0     | 0.10   |
| Micron    | 1100 SATA          | 512 GB | 1       | 36    | 0     | 0.10   |
| ADATA     | SU750              | 256 GB | 1       | 36    | 0     | 0.10   |
| Transcend | TS32GMSA370        | 32 GB  | 3       | 35    | 0     | 0.10   |
| Phison    | SATA SSD           | 64 GB  | 1       | 33    | 0     | 0.09   |
| OCZ       | VERTEX-TURBO       | 32 GB  | 2       | 298   | 56    | 0.09   |
| Apacer    | AS350              | 256 GB | 1       | 30    | 0     | 0.08   |
| Crucial   | CT480M500SSD1      | 480 GB | 1       | 580   | 20    | 0.08   |
| WDC       | WDS120G2G0B-00EPW0 | 120 GB | 1       | 26    | 0     | 0.07   |
| Kingston  | SHSS37A240G        | 240 GB | 1       | 25    | 0     | 0.07   |
| Crucial   | CT240BX500SSD1     | 240 GB | 2       | 23    | 0     | 0.06   |
| KingFast  | SSD                | 512 GB | 1       | 23    | 0     | 0.06   |
| China     | CS2246-M512        | 506 GB | 1       | 22    | 0     | 0.06   |
| SanDisk   | SSD PLUS           | 240 GB | 2       | 43    | 1     | 0.06   |
| Transcend | TS512GMSA370       | 512 GB | 1       | 21    | 0     | 0.06   |
| Micron    | MTFDDAV256MBF-1... | 256 GB | 1       | 21    | 0     | 0.06   |
| SanDisk   | SSD i100           | 64 GB  | 1       | 21    | 0     | 0.06   |
| China     | SATA SSD           | 256 GB | 1       | 21    | 0     | 0.06   |
| ORICO     | PH100-128G         | 128 GB | 1       | 19    | 0     | 0.05   |
| ADATA     | SU650              | 120 GB | 2       | 406   | 106   | 0.05   |
| Samsung   | MZNLN256HAJQ-000L7 | 256 GB | 1       | 14    | 0     | 0.04   |
| Transcend | TS256GMTS400       | 256 GB | 1       | 14    | 0     | 0.04   |
| Intel     | SSDSC2BF180A5H REF | 180 GB | 1       | 13    | 0     | 0.04   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 1       | 13    | 0     | 0.04   |
| PNY       | SSD2SC240G5LC70... | 240 GB | 1       | 13    | 0     | 0.04   |
| KingSpec  | NT-512             | 512 GB | 1       | 12    | 0     | 0.04   |
| Lite-On   | LCH-256V2S         | 256 GB | 1       | 12    | 0     | 0.03   |
| Transcend | TS128GMSA370       | 128 GB | 1       | 11    | 0     | 0.03   |
| Intenso   | SSD Sata III       | 240 GB | 1       | 10    | 0     | 0.03   |
| Dogfish   | SSD                | 64 GB  | 1       | 10    | 0     | 0.03   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 1       | 10    | 0     | 0.03   |
| Leven     | JAJS600M512C       | 512 GB | 1       | 9     | 0     | 0.03   |
| Transcend | TS128GMTS430S      | 128 GB | 1       | 8     | 0     | 0.02   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 26      | 8     | 0     | 0.02   |
| Intenso   | SSD Sata III       | 128 GB | 2       | 7     | 26    | 0.02   |
| Micron    | 1100 SATA          | 256 GB | 1       | 22    | 2     | 0.02   |
| Apple     | SSD SM256E         | 256 GB | 1       | 809   | 122   | 0.02   |
| Lexar     | 256GB SSD          | 256 GB | 1       | 6     | 0     | 0.02   |
| Crucial   | M4-CT128M4SSD3     | 128 GB | 1       | 4     | 0     | 0.01   |
| Apacer    | AS350              | 128 GB | 1       | 4     | 0     | 0.01   |
| Team      | T253X1240G         | 240 GB | 1       | 4     | 0     | 0.01   |
| Kingston  | SHFS37A240G        | 240 GB | 1       | 4     | 0     | 0.01   |
| Mushkin   | MKNSSDSR120GB      | 120 GB | 1       | 3     | 0     | 0.01   |
| Innodisk  | 2.5" SATA SSD 3... | 128 GB | 1       | 3     | 0     | 0.01   |
| OWC       | Aura               | 960 GB | 1       | 3     | 0     | 0.01   |
| SK hynix  | SC210 mSATA        | 256 GB | 1       | 391   | 139   | 0.01   |
| Transcend | TS120GMTS420S      | 120 GB | 2       | 2     | 0     | 0.01   |
| Kingston  | SV300S37A60G       | 64 GB  | 1       | 1586  | 804   | 0.01   |
| Samsung   | MZNLH512HALU-00000 | 512 GB | 1       | 1     | 0     | 0.01   |
| Intel     | SSDSC2BA200G3T     | 200 GB | 2       | 1873  | 1028  | 0.00   |
| Intel     | SSDSCKKF256G8H     | 256 GB | 1       | 144   | 89    | 0.00   |
| Samsung   | MZHPV512HDGL-00000 | 512 GB | 1       | 1     | 0     | 0.00   |
| Samsung   | SSD UM410 Serie... | 16 GB  | 1       | 38    | 24    | 0.00   |
| China     | MSATA 64GB SSD     | 64 GB  | 1       | 1     | 0     | 0.00   |
| Kingston  | SNS4151S316G       | 16 GB  | 1       | 1252  | 1022  | 0.00   |
| Intel     | SSDSC2CW120A3      | 120 GB | 1       | 1235  | 1019  | 0.00   |
| Lite-On   | LCH-128V2S         | 128 GB | 1       | 1     | 0     | 0.00   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SD7UB3Q256G1001    | 256 GB | 1       | 84    | 100   | 0.00   |
| Kingston  | RBU-SNS4151S316GG2 | 16 GB  | 1       | 0     | 0     | 0.00   |
| FORESEE   | 64GB SSD           | 64 GB  | 1       | 0     | 0     | 0.00   |
| QUMO      | SSD                | 120 GB | 1       | 0     | 0     | 0.00   |
| SanDisk   | SSD G5 BICS4       | 500 GB | 1       | 0     | 0     | 0.00   |
| Zheino    | CHN-mSATAQ3-120    | 120 GB | 1       | 0     | 0     | 0.00   |
| Intel     | SSDSC2KW120H6      | 120 GB | 1       | 2     | 29    | 0.00   |
| Kingston  | SNS4151S332G       | 32 GB  | 1       | 79    | 1022  | 0.00   |
| Micron    | MTFDDAK256MAM-1K12 | 256 GB | 1       | 52    | 1010  | 0.00   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 39    | 1010  | 0.00   |
| Micron    | MTFDDAT128MAM-1J2  | 128 GB | 1       | 28    | 1587  | 0.00   |

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
| OCZ       | SandForce Driven SSDs  | 4      | 5       | 1701  | 0     | 4.66   |
| ADATA     | SandForce Driven SSDs  | 1      | 1       | 1548  | 0     | 4.24   |
| SK hynix  | Unknown                | 1      | 1       | 1542  | 0     | 4.22   |
| Intel     | 330/335 Series SSDs    | 2      | 3       | 2131  | 3     | 3.95   |
| Intel     | 320 Series SSDs        | 3      | 4       | 1213  | 0     | 3.32   |
| SuperM... | Silicon Motion base... | 1      | 1       | 1176  | 0     | 3.22   |
| ADATA     | JMicron based SSDs     | 4      | 4       | 1129  | 0     | 3.09   |
| Intel     | X18-M/X25-M/X25-V G... | 3      | 3       | 2090  | 3     | 3.03   |
| Transcend | JMicron based SSDs     | 1      | 1       | 1067  | 0     | 2.92   |
| Goodram   | Phison Driven OEM SSDs | 2      | 3       | 1063  | 0     | 2.91   |
| Crucial   | Unknown                | 1      | 2       | 1042  | 0     | 2.86   |
| WDC       | Blue / Red / Green ... | 2      | 3       | 1022  | 0     | 2.80   |
| Seagate   | Unknown                | 1      | 1       | 1781  | 1     | 2.44   |
| Intel     | 53x and Pro 1500/25... | 3      | 4       | 874   | 0     | 2.39   |
| Toshiba   | HG3 Series             | 1      | 1       | 826   | 0     | 2.26   |
| Micron    | 5100 Pro / 5200 SSDs   | 1      | 4       | 778   | 0     | 2.13   |
| MyDigi... | Unknown                | 1      | 1       | 763   | 0     | 2.09   |
| Apple     | JMicron based SSDs     | 1      | 1       | 752   | 0     | 2.06   |
| Samsung   | Samsung based SSDs     | 52     | 126     | 710   | 1     | 1.89   |
| Toshiba   | HG6 Series SSD         | 3      | 5       | 683   | 0     | 1.87   |
| OWC       | SandForce Driven SSDs  | 1      | 1       | 657   | 0     | 1.80   |
| SanDisk   | SanDisk based SSDs     | 4      | 6       | 656   | 17    | 1.76   |
| SPCC      | Unknown                | 1      | 1       | 617   | 0     | 1.69   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 8       | 600   | 1     | 1.64   |
| Kingston  | SandForce Driven SSDs  | 11     | 19      | 836   | 44    | 1.57   |
| SanDisk   | SandForce Driven SSDs  | 1      | 2       | 566   | 0     | 1.55   |
| Intel     | 730 and DC S35x0/36... | 6      | 7       | 1102  | 294   | 1.42   |
| Crucial   | BX/MX1/2/3/500, M5/... | 9      | 23      | 530   | 1     | 1.34   |
| Plextor   | M3/M5/M6/M7 Series ... | 1      | 1       | 483   | 0     | 1.32   |
| SanDisk   | Marvell based SanDi... | 15     | 28      | 584   | 4     | 1.24   |
| AEGO      | Unknown                | 1      | 1       | 445   | 0     | 1.22   |
| Kingston  | SSDNow UV400/500       | 5      | 14      | 429   | 0     | 1.18   |
| Phison    | Driven OEM SSDs        | 5      | 13      | 428   | 0     | 1.17   |
| Corsair   | SandForce Driven SSDs  | 2      | 3       | 988   | 1     | 1.17   |
| Intel     | 520 Series SSDs        | 3      | 4       | 1395  | 509   | 1.17   |
| Intel     | Unknown                | 5      | 7       | 493   | 14    | 1.14   |
| Samsung   | Unknown                | 7      | 10      | 378   | 3     | 1.03   |
| Mushkin   | Unknown                | 2      | 2       | 369   | 0     | 1.01   |
| Kingston  | Phison Driven SSDs     | 6      | 26      | 342   | 0     | 0.94   |
| Crucial   | RealSSD m4/C400/P400   | 2      | 2       | 296   | 0     | 0.81   |
| Hoodisk   | Phison Driven OEM SSDs | 2      | 5       | 295   | 0     | 0.81   |
| Vaseky    | Unknown                | 2      | 2       | 293   | 0     | 0.81   |
| SPCC      | Phison Driven OEM SSDs | 3      | 4       | 287   | 0     | 0.79   |
| Patriot   | Phison Driven SSDs     | 2      | 2       | 285   | 0     | 0.78   |
| SanDisk   | Unknown                | 10     | 10      | 274   | 0     | 0.75   |
| Plextor   | Unknown                | 1      | 1       | 230   | 0     | 0.63   |
| OCZ       | Indilinx Barefoot_2... | 3      | 3       | 523   | 2     | 0.54   |
| China     | Unknown                | 8      | 8       | 191   | 0     | 0.52   |
| PNY       | Phison Driven SSDs     | 1      | 4       | 189   | 0     | 0.52   |
| KingDian  | Unknown                | 1      | 1       | 177   | 0     | 0.49   |
| ZTC       | Unknown                | 1      | 1       | 164   | 0     | 0.45   |
| SK hynix  | SATA SSDs              | 4      | 4       | 393   | 36    | 0.45   |
| Crucial   | BX/MX1/2/3/500, M5/... | 3      | 5       | 273   | 4     | 0.45   |
| Kingston  | Unknown                | 8      | 8       | 393   | 257   | 0.44   |
| Apacer    | SDM5/5A/5A-M Series... | 1      | 1       | 1769  | 10    | 0.44   |
| Crucial   | MX500 SSDs             | 4      | 10      | 155   | 0     | 0.43   |
| Toshiba   | Unknown                | 1      | 2       | 131   | 0     | 0.36   |
| KingDian  | Silicon Motion base... | 3      | 4       | 128   | 0     | 0.35   |
| Verbatim  | Unknown                | 1      | 1       | 115   | 0     | 0.32   |
| Transcend | Silicon Motion base... | 11     | 16      | 115   | 0     | 0.32   |
| Intel     | Dell Certified Inte... | 1      | 2       | 105   | 0     | 0.29   |
| Apple     | SD/SM/TS E/F/G SSDs    | 4      | 5       | 250   | 25    | 0.25   |
| ADATA     | Silicon Motion base... | 2      | 2       | 84    | 0     | 0.23   |
| KingSpec  | Unknown                | 2      | 2       | 76    | 0     | 0.21   |
| WDC       | Blue and Green SSDs    | 11     | 46      | 75    | 1     | 0.20   |
| Apacer    | Unknown                | 3      | 3       | 74    | 0     | 0.20   |
| Intel     | S4510/S4610/S4500/S... | 1      | 3       | 70    | 0     | 0.19   |
| Lite-On   | Unknown                | 4      | 4       | 70    | 0     | 0.19   |
| Plextor   | M3/M5/M6 Series SSDs   | 1      | 2       | 64    | 0     | 0.18   |
| OCZ       | OCZ/Toshiba Trion SSDs | 1      | 1       | 40    | 0     | 0.11   |
| KingFast  | Unknown                | 2      | 3       | 32    | 0     | 0.09   |
| OCZ       | Indilinx Barefoot b... | 1      | 2       | 298   | 56    | 0.09   |
| ADATA     | Unknown                | 3      | 4       | 224   | 53    | 0.08   |
| Micron    | BX/MX1/2/3/500, M5/... | 1      | 1       | 21    | 0     | 0.06   |
| ORICO     | Unknown                | 1      | 1       | 19    | 0     | 0.05   |
| PNY       | Unknown                | 1      | 1       | 13    | 0     | 0.04   |
| Dogfish   | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| Leven     | Unknown                | 1      | 1       | 9     | 0     | 0.03   |
| Intenso   | Unknown                | 2      | 3       | 8     | 17    | 0.02   |
| Lexar     | Unknown                | 1      | 1       | 6     | 0     | 0.02   |
| Team      | Unknown                | 1      | 1       | 4     | 0     | 0.01   |
| Innodisk  | 3IE2/3ME2/3MG2/3SE2... | 1      | 1       | 3     | 0     | 0.01   |
| OWC       | Unknown                | 1      | 1       | 3     | 0     | 0.01   |
| FORESEE   | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| QUMO      | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Zheino    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |
| Intel     | 540 Series SSDs        | 2      | 2       | 20    | 520   | 0.00   |
| Micron    | RealSSD m4/C400/P400   | 1      | 1       | 52    | 1010  | 0.00   |
| Micron    | Unknown                | 1      | 1       | 28    | 1587  | 0.00   |

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
| SuperMicro  | 1      | 1       | 1176  | 0     | 3.22   |
| Goodram     | 2      | 3       | 1063  | 0     | 2.91   |
| Seagate     | 1      | 1       | 1781  | 1     | 2.44   |
| OCZ         | 9      | 11      | 974   | 11    | 2.29   |
| MyDigita... | 1      | 1       | 763   | 0     | 2.09   |
| Samsung     | 59     | 136     | 686   | 1     | 1.83   |
| Intel       | 29     | 39      | 980   | 135   | 1.73   |
| ADATA       | 10     | 11      | 648   | 20    | 1.58   |
| Toshiba     | 5      | 8       | 563   | 0     | 1.54   |
| Micron      | 9      | 15      | 534   | 174   | 1.45   |
| AEGO        | 1      | 1       | 445   | 0     | 1.22   |
| SanDisk     | 30     | 46      | 525   | 5     | 1.21   |
| SK hynix    | 5      | 5       | 623   | 29    | 1.20   |
| Phison      | 5      | 13      | 428   | 0     | 1.17   |
| Corsair     | 2      | 3       | 988   | 1     | 1.17   |
| Kingston    | 30     | 67      | 507   | 43    | 1.11   |
| Crucial     | 19     | 42      | 423   | 1     | 1.06   |
| Mushkin     | 2      | 2       | 369   | 0     | 1.01   |
| SPCC        | 4      | 5       | 353   | 0     | 0.97   |
| OWC         | 2      | 2       | 330   | 0     | 0.90   |
| Hoodisk     | 2      | 5       | 295   | 0     | 0.81   |
| Vaseky      | 2      | 2       | 293   | 0     | 0.81   |
| Patriot     | 2      | 2       | 285   | 0     | 0.78   |
| Plextor     | 3      | 4       | 210   | 0     | 0.58   |
| Apple       | 5      | 6       | 334   | 21    | 0.55   |
| China       | 8      | 8       | 191   | 0     | 0.52   |
| Transcend   | 12     | 17      | 171   | 0     | 0.47   |
| ZTC         | 1      | 1       | 164   | 0     | 0.45   |
| PNY         | 2      | 5       | 154   | 0     | 0.42   |
| KingDian    | 4      | 5       | 138   | 0     | 0.38   |
| WDC         | 13     | 49      | 133   | 1     | 0.36   |
| Verbatim    | 1      | 1       | 115   | 0     | 0.32   |
| Apacer      | 4      | 4       | 497   | 3     | 0.26   |
| KingSpec    | 2      | 2       | 76    | 0     | 0.21   |
| Lite-On     | 4      | 4       | 70    | 0     | 0.19   |
| KingFast    | 2      | 3       | 32    | 0     | 0.09   |
| ORICO       | 1      | 1       | 19    | 0     | 0.05   |
| Dogfish     | 1      | 1       | 10    | 0     | 0.03   |
| Leven       | 1      | 1       | 9     | 0     | 0.03   |
| Intenso     | 2      | 3       | 8     | 17    | 0.02   |
| Lexar       | 1      | 1       | 6     | 0     | 0.02   |
| Team        | 1      | 1       | 4     | 0     | 0.01   |
| Innodisk    | 1      | 1       | 3     | 0     | 0.01   |
| FORESEE     | 1      | 1       | 0     | 0     | 0.00   |
| QUMO        | 1      | 1       | 0     | 0     | 0.00   |
| Zheino      | 1      | 1       | 0     | 0     | 0.00   |

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
| Samsung   | SSD 950 PRO        | 512 GB | 2       | 1098  | 0     | 3.01   |
| Samsung   | MZVPV256HDGL-000L7 | 256 GB | 1       | 915   | 0     | 2.51   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 1       | 637   | 0     | 1.75   |
| Samsung   | SSD 960 EVO        | 250 GB | 3       | 612   | 0     | 1.68   |
| Plextor   | PX-256M8PeG        | 256 GB | 1       | 598   | 0     | 1.64   |
| HP        | SSD EX900          | 120 GB | 1       | 591   | 0     | 1.62   |
| HP        | SSD EX920          | 512 GB | 1       | 531   | 0     | 1.46   |
| Patriot   | Scorch M2          | 128 GB | 1       | 493   | 0     | 1.35   |
| Samsung   | SSD 970 PRO        | 512 GB | 1       | 466   | 0     | 1.28   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 1       | 456   | 0     | 1.25   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 1       | 405   | 0     | 1.11   |
| Intel     | SSDPEKKF256G8L     | 256 GB | 1       | 376   | 0     | 1.03   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 1       | 363   | 0     | 1.00   |
| Corsair   | Force MP600        | 2 TB   | 1       | 308   | 0     | 0.85   |
| Intel     | SSDPED1D480GA      | 480 GB | 1       | 299   | 0     | 0.82   |
| SPCC      | M.2 PCIe SSD       | 512 GB | 2       | 297   | 0     | 0.81   |
| Samsung   | SSD 960 EVO        | 500 GB | 1       | 264   | 0     | 0.72   |
| WDC       | WDS500G1B0C-00S6U0 | 500 GB | 1       | 257   | 0     | 0.71   |
| Toshiba   | THNSF5256GPUK      | 256 GB | 1       | 247   | 0     | 0.68   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 1       | 239   | 0     | 0.66   |
| ADATA     | SX8200PNP          | 1 TB   | 2       | 228   | 0     | 0.63   |
| Samsung   | MZVLB512HAJQ-000L7 | 512 GB | 4       | 252   | 1     | 0.53   |
| Intel     | SSDPEDMW800G4      | 800 GB | 1       | 168   | 0     | 0.46   |
| Toshiba   | RC100              | 240 GB | 1       | 151   | 0     | 0.41   |
| ORICO     | V500               | 1 TB   | 1       | 149   | 0     | 0.41   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 1       | 137   | 0     | 0.38   |
| Toshiba   | THNSF5256GCJ7      | 256 GB | 1       | 130   | 0     | 0.36   |
| Samsung   | PM961 NVMe         | 512 GB | 1       | 116   | 0     | 0.32   |
| Crucial   | CT1000P1SSD8       | 1 TB   | 5       | 111   | 0     | 0.30   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 1       | 109   | 0     | 0.30   |
| Corsair   | Force MP300        | 120 GB | 1       | 102   | 0     | 0.28   |
| Corsair   | Force MP600        | 500 GB | 1       | 91    | 0     | 0.25   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 2       | 89    | 0     | 0.24   |
| Samsung   | SSD 970 PRO        | 1 TB   | 2       | 83    | 0     | 0.23   |
| Intel     | HBRPEKNX0202AHO    | 32 GB  | 1       | 81    | 0     | 0.22   |
| Intel     | HBRPEKNX0202AH     | 512 GB | 1       | 80    | 0     | 0.22   |
| Samsung   | MZVLB512HBJQ-000L7 | 512 GB | 2       | 79    | 0     | 0.22   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 5       | 67    | 0     | 0.19   |
| SK hynix  | BC501 HFM256GDJ... | 256 GB | 2       | 60    | 0     | 0.17   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 2       | 51    | 0     | 0.14   |
| Intel     | SSDPEKNW512G8      | 512 GB | 1       | 46    | 0     | 0.13   |
| Samsung   | SSD 970 EVO        | 500 GB | 1       | 42    | 0     | 0.12   |
| Samsung   | PM981 NVMe         | 256 GB | 1       | 40    | 0     | 0.11   |
| Samsung   | SSD 960 EVO        | 1 TB   | 1       | 154   | 3     | 0.11   |
| Phison    | Sabrent Rocket 4.0 | 1 TB   | 1       | 36    | 0     | 0.10   |
| WDC       | PC SN730 SDBQNT... | 512 GB | 1       | 32    | 0     | 0.09   |
| WDC       | PC SN730 SDBQNT... | 1 TB   | 1       | 32    | 0     | 0.09   |
| Intel     | SSDPEKKF512G8L     | 512 GB | 2       | 30    | 0     | 0.08   |
| Kingston  | RBUSNS8154P3512GJ  | 512 GB | 1       | 25    | 0     | 0.07   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 1       | 23    | 0     | 0.06   |
| SK hynix  | PC401 NVMe         | 256 GB | 1       | 22    | 0     | 0.06   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 1       | 18    | 0     | 0.05   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 1       | 17    | 0     | 0.05   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 1       | 13    | 0     | 0.04   |
| Lite-On   | CA3-8D512          | 512 GB | 1       | 10    | 0     | 0.03   |
| Phison    | PCIe SSD           | 512 GB | 1       | 10    | 0     | 0.03   |
| Micron    | 2200V_MTFDHBA51... | 512 GB | 1       | 7     | 0     | 0.02   |
| Union ... | UMIS LENSE40512... | 512 GB | 1       | 6     | 0     | 0.02   |
| Samsung   | MZVLQ256HAJD-00000 | 256 GB | 1       | 5     | 0     | 0.02   |
| Samsung   | MZVLW512HMJP-00000 | 512 GB | 1       | 5     | 0     | 0.02   |
| WDC       | PC SN520 SDAPNU... | 512 GB | 1       | 5     | 0     | 0.01   |
| Toshiba   | KBG30ZMT512G       | 512 GB | 1       | 2     | 0     | 0.01   |
| Union ... | RPFTJ128PDD2EWX    | 128 GB | 1       | 1     | 0     | 0.00   |
| SK hynix  | HFM256GDJTNG-8310A | 256 GB | 1       | 1     | 0     | 0.00   |
| Toshiba   | KXG60PNV2T04 NV... | 2 TB   | 1       | 0     | 0     | 0.00   |
| ADATA     | SX6000LNP          | 512 GB | 1       | 0     | 0     | 0.00   |
| SK hynix  | SKHynix_HFS512G... | 512 GB | 1       | 0     | 0     | 0.00   |

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
| Plextor     | 1      | 1       | 598   | 0     | 1.64   |
| HP          | 2      | 2       | 561   | 0     | 1.54   |
| Patriot     | 1      | 1       | 493   | 0     | 1.35   |
| Samsung     | 21     | 34      | 257   | 1     | 0.68   |
| SPCC        | 2      | 4       | 193   | 0     | 0.53   |
| Intel       | 8      | 9       | 168   | 0     | 0.46   |
| Corsair     | 4      | 4       | 152   | 0     | 0.42   |
| ADATA       | 2      | 3       | 152   | 0     | 0.42   |
| Toshiba     | 6      | 6       | 149   | 0     | 0.41   |
| ORICO       | 1      | 1       | 149   | 0     | 0.41   |
| WDC         | 7      | 7       | 135   | 0     | 0.37   |
| Crucial     | 1      | 5       | 111   | 0     | 0.30   |
| SK hynix    | 4      | 5       | 28    | 0     | 0.08   |
| Kingston    | 1      | 1       | 25    | 0     | 0.07   |
| Phison      | 2      | 2       | 23    | 0     | 0.07   |
| Lite-On     | 1      | 1       | 10    | 0     | 0.03   |
| Micron      | 1      | 1       | 7     | 0     | 0.02   |
| Union Me... | 2      | 2       | 4     | 0     | 0.01   |

