# statistic

<b>HOW TO RUN</b>

Build and run using gradle (https://gradle.org):
  - clone the project to local folder
  - init gradle by running `[ROOT_FOLDER]/gradle wrapper`
  - build with `[ROOT_FOLDER]/gradlew build`;
  - find statistic.war file in `[ROOT_FOLDER]/build/libs` folder
  - deploy war file to servlet container, e.g. Tomcat, runnint at `[HOST]` with `[PORT]`
  - access API at:
    - `GET ~ http://[HOST]:[PORT]/statistic/api/statistics` 
    - `POST ~ http://[HOST]:[PORT]/statistic/api/transactions`

<b>CONSTANT TIME SOLUTION</b>

Constant run time and memory usage solution is achieved by storing aggregated statistic for every of past 60 seconds.
Storage content is updated whenever next valid transaction is logged to start with the most recent (current) moment and keep history of last 60 seconds.
Transactions older than 60 seconds or with timestamp in the future are ignored. When transaction with the timestamp withing last 60 seconds is logged aggregated statistic for the second is updated with its amount.
When statistic for the past 60 seconds is requested aggregated statistic is build using stored statistics for the seconds in the requested time range.

O(c) complexity is achieved because:
  - we only store 60 aggregated statistics at any time;
  - to retrieve statistic we do 60 actions at most - retrieving statistic for a second;
  - to log new transacton we do 60 actions at most - removing outdated statistics and placing new ones.

