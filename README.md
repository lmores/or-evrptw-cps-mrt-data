# The Electric Vehicle Routing Problem with Capacitated Public Stations and Multiple Recharging Technologies

This repository contains data related to the scientific article 'The Electric Vehicle Routing Problem with Capacitated Public Stations and Multiple Recharging Technologies' by Bruglieri Maurizio and Moreschini Lorenzo currently submitted for publication on Transportation Science.


## Instance format

The data for each of the 224 instances are stored in JSON files with the following format.

  - `name` (string): instance name following the format`(c|r|rc)(1|2)xx_cs_ch`, where:
    + `c|r|rc` refers to the method used to generate customers' locations; `c` means 'clustered', `r` means 'random', `rc` means 'random and clustered',
    + `1|2`: is the subfamily the instance belongs to; in each subfamily customers' locations are fixed and the other parameters (customers' time windows, number of stations, ...) vary,
    + `xx`: is the identifier of the instance within its subfamily,
    + `cs`: is the number of customers,
    + `ch`: is the number of chargers (either 1 or 2).

  - `nCustomers` (int): the number of customers.

  - `nStations` (int): the number of stations.

  - `loadCapacity` (int): the load capacity of a vehicle.

  - `batteryCapacity` (int): the battery capacity of a vehicle.

  - `maxTime` (int): the end of the planning horizon.

  - `consumptionRate` (double): the energy required to travel a distance of 1 unit.

  - `depotRechargeCost` (double): the unit-energy recharge cost at the depot.

  - `customerDemands` (int[]): an array with `nCustomers` entries representing the demand of each customer.

  - `customerServiceTimes` (int[]): an array with `nCustomers` entries representing the service time of each customer.

  - `customerStarts` (int[]): an array with `nCustomers` entries representing the earliest service start time of each customer.

  - `customerEnds` (int[]): an array with `nCustomers` entries representing the latest service start time of each customer.

  - `stationNChargers` (int[]): an array with `nStations` entries representing the number of chargers available in each station.

  - `chargerTimeWindows` (int[][][]): an array with a number of entries equal to the total number of chargers among all stations (i.e. the sum of all entries in `stationNChargers`).
    The time windows of each charger are encoded as an array of intervals (each represented by an array of size 2).
    This array first contains the time windows of the chargers at the first station, followed by those at the second station, and so on.

  - `chargerCosts` (double[]):  an array with a number of entries equal to the total number of chargers among all stations (i.e. the sum of all entries in `stationNChargers`) representing the unit-energy recharge cost of each charger.
    This array first contains the costs of chargers at the first station, followed by those at the second station, and so on.

  - `chargerProfiles` (double[][][]): an array with a number of entries equal to the total number of chargers among all stations (i.e. the sum of all entries in `stationNChargers`).
    This array first contains the charging function/profiles of the chargers at the first station, followed by those at the second station, and so on.
    Each function/profile is represented as an array of pairs [time, energy] (i.e., 2-element arrays), corresponding to the breakpoints of the piecewise linear function that models the recharging process at a charger.
    Since recharging is assumed to be linear over time, each piecewise linear function reduces to a linear function defined by exactly two break points: `[0, 0]` and `[rechargeTime, batteryCapacity]`, where `rechargeTime` denotes the time required to fully recharge a depleted battery.

  - `travelDistances` (double[][]): a square matrix containing distances among customers, the depot and stations.
    The order of rows/columns is the following: first `nCustomers` rows/columns corresponding to customers, then the depot, and then `nStations` rows/columns corresponding to stations.

  - `travelTimes` (double[][]):  a square matrix containing travel times among customers, the depot and stations, with the same layout as `travelDistances`.

  - `xCoords` (double[]): the x coodinates of customers, depot and stations in the same order as the rows/columns of the `travelDistances` matrix.

  - `yCoords` (double[]): the y coodinates of customers, depot and stations in the same order as the rows/columns of the `travelDistances` matrix.

**NB:** the single source of truth for distances and travel times are the `travelDistances` and `travelTimes` matrices.
`xCoords` and `yCoords` are available only to represent customers, depot and stations on a map.
In particular, values contained in `travelDistances` and `travelTimes` have been computed as in [Lam et. all 2022][lam2022] by rouding to the smallest integer greater than or equal to the euclidean distance between each pair of points.



[lam2022]: <https://doi.org/10.1016/j.cor.2022.105870> "Edward Lam, Guy Desaulniers, Peter J. Stuckey, 'Branch-and-cut-and-price for the Electric Vehicle Routing Problem with Time Windows, Piecewise-Linear Recharging and Capacitated Recharging Stations', Computers & Operations Research, Volume 145, 2022, 105870, ISSN 0305-0548, https://doi.org/10.1016/j.cor.2022.105870"
