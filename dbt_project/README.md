Welcome to your new dbt project!

### Example Data Flow

Clone the git repo and start the data warehouse docker container

``` shell
docker compose up -d
```

#### Run dbt

``` shell
export DBT_PROFILES_DIR=$(pwd)
cd sde_dbt_tutorial
dbt snapshot
dbt run
dbt test
dbt docs generate
dbt docs serve
```

#### Insert updates into source customer table, to demonstrate snapshot

``` shell
pgcli -h localhost -U dbt -p 5432 -d dbt
# password is password1234
COPY warehouse.customers(customer_id, zipcode, city, state_code, datetime_created, datetime_updated) FROM '/input_data/customer_new.csv' DELIMITER ',' CSV HEADER;
\q
```

#### Run snapshot and create models again.

``` shell
dbt snapshot
dbt run
```

You can log into the data warehouse to see the models.

``` shell
pgcli -h localhost -U dbt -p 5432 -d dbt
# password is password1234
select * from warehouse.customer_orders limit 3;
\q
```

#### Stop docker container

``` shell
cd ..
docker compose down
````


### Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](http://slack.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices