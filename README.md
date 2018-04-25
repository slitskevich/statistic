# statistic

<b>HOW TO RUN</b>

Build and run using gradle (https://gradle.org):
  - clone the project to local folder
  - init gradle by running `[ROOT_FOLDER]/gradle wrapper`
  - build with '[ROOT_FOLDER]/gradlew build';
  - find statistic.war file in '[ROOT_FOLDER]/build/libs' folder
  - deploy war file to servlet container, e.g. Tomcat
  - access API at:
    - GET ~ http://[HOST]:[PORT]/statistic/api/statistics 
    - POST ~ http://[HOST]:[PORT]/statistic/api/transactions

<b>CONSTANT TIME SOLUTION</b>

Constant run time and memory usage solution is achieved by storing aggregated statistic for every of past 60 seconds.
Storage content is updated whenever next valid transaction is logged. 
Transactions with timestamp in the future are ignored.
