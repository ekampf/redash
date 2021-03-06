# [_re:dash_](https://github.com/everythingme/redash)

**_re:dash_** is our take on freeing the data within our company in a way that will better fit our culture and usage patterns.

Prior to **_re:dash_**, we tried to use tranditional BI suites and discovered a set of bloated, technically challenged and slow tools/flows. What we were looking for was a more hacker'ish way to look at data, so we built one.

**_re:dash_** was built to allow fast and easy access to billions of records, that we process and collect using Amazon Redshift ("petabyte scale data warehouse" that "speaks" PostgreSQL).

**_re:dash_** consists of two parts:

1. **Query Editor**: think of [JS Fiddle](http://jsfiddle.net) for SQL queries. It's your way to share data in the organization in an open way, by sharing both the dataset and the query that generated it. This way everyone can peer review not only the resulting dataset but also the process that generated it. Also it's possible to fork it and generate new datasets and reach new insights. 
2. **Dashboards/Visualizations**: once you have a dataset, you can create different visualizations out of it, and then combine several visualizations into a single dashboard. Currently it supports bar charts, pivot table and cohorts.

This is the first release, which is more than usable but still has its rough edges and way to go to fulfill its full potential. The Query Editor part is quite solid, but the visualizations need more work to enrich them and to make them more user friendly.

## Demo

![Screenshots](https://raw.github.com/EverythingMe/redash/screenshots/screenshots.gif)

You can try out the demo instance: http://rd-demo.herokuapp.com/ (login with any Google account).

Due to Heroku dev plan limits, it has a small database of flights (see schema [here](http://rd-demo.herokuapp.com/dashboard/schema)). Also due to another Heroku limitation, it is running with the regular user, hence you can DELETE or INSERT data/tables. Please be nice and don't do this.

## Technology

* [AngularJS](http://angularjs.org/)
* [Tornado](http://tornadoweb.org)
* [PostgreSQL](http://www.postgresql.org/) / [AWS Redshift](http://aws.amazon.com/redshift/)
* [Redis](http://redis.io)

PostgreSQL is used both as the operatinal database for the system, but also as the data store that is being queried. To be exact, we built this system to use on top of Amazon's Redshift, which supports the PG driver. But it's quite simple to add support for other datastores, and we do plan to do so.

This is our first large scale AngularJS project, and we learned a lot during the development of it. There are still things we need to iron out, and comments on the way we use AngularJS are more than welcome (and pull requests just as well).

### HighCharts

HighCharts is really great, but it's not free for commercial use. Please refer to their [licensing options](http://shop.highsoft.com/highcharts.html), to see what applies for your use. 

It's very likely that in the future we will switch to [D3.js](http://d3js.org/) instead.

## Getting Started

1. Clone the repo:
```bash
git clone git@github.com:EverythingMe/redash.git
```
2. Create settings file from the example one (& update relevant settings):
```bash
cp rd_service/settings_example.py rd_service/settings.py
```
It's highly recommended that the user you use to connect to the data database (the one you query) is read-only.
3. Create the operational databases from rd_service/data/tables.sql
3. Install `npm` packages (mainly: Bower & Grunt):
```bash
cd rd_ui
npm install
```
4. Install `bower` packages:
```bash
bower install
```
5. Build the UI:
```bash
grunt build
```
6. Install PIP packages:
```bash
pip install -r ../rd_service/requirements.txt
```
6. Start the API server:
```bash
cd ../rd_service
python server.py
```
7. Start the workers:
```bash
python cli.py worker
```
8. Open `http://localhost:8888/` and query away.

## Roadmap

We plan to release new minor version every 2-3 weeks. Of course, if we get additional help from contributors it will help speed things up.

Below you can see the "big" features of the next 3 releases (for full list, click on the link):

### [v0.2](https://github.com/EverythingMe/redash/issues?milestone=1&state=open)

- Ability to generate multiple visualizations for a single query (dataset) in a more flexible way than today. Also easier extensbility points to add additional visualizations.
- Dashboard filters: ability to filter/slice the data you see in a single dashboard using filters (date or selectors).
- UI Improvements (better notifications & flows, improved queries page) 
- Comments on queries.

### [v0.3](https://github.com/EverythingMe/redash/issues?milestone=2&state=open)

- Support for API access using API keys, instead of Google Login.
- Multiple databases support (including other database type than PostgreSQL).
- Scheduled reports by email.

### [v0.4](https://github.com/EverythingMe/redash/issues?milestone=3&state=open)

- Query versioning. 
- More "realtime" UI (using websockets).
- More visualizations.

## Reporting Bugs and Contributing Code

* Want to report a bug or request a feature? Please open [an issue](https://github.com/everythingme/redash/issues/new).
* Want to help us build **_re:dash_**? Fork the project and make a pull request. We need all the help we can get!

## License

See [LICENSE](https://github.com/EverythingMe/redash/blob/master/LICENSE) file.
