# psusannx_betfair

A package that allows an easy connection to the [Betfair Exchange API](https://www.betfair.com/exchange/plus/), provided valid credentials are given. The package contains a class which stores the credentials provided, and allows the user to get basic **delayed (~3mins)** market odds information on premier league matches. The current version of the package only allows getting odds for matches that are listed on the betfair exchange at the time of running the function. There is no feature for getting odds on historical matches yet.

For more information on getting started with the Betfair API, read through the [Getting Started](https://docs.developer.betfair.com/display/1smk3cen4v3lu3yomq5qye0ni/Getting+Started) docs.

This package was created to be used as a subpackage in a wider project - PSUSANNX.

## Package Functions

- list_upcoming_pl_matches()
- get_betfair_exchange_odds()

## Installation

```python
pip install psusannx_betfair
```

## Usage

```python
# Import the package
import psusannx_betfair

# Get some info about the class object
help(psusannx_betfair.PsusannxBetfair) 
```

Once the class has been imported and you've read the help, you can create an instance of the class to allow you to interact with your betfair account through the API. Make sure you have the required credentials at hand. You need the following information & you need to follow the steps in the links to use the class properly:

- Betfair username
- Betfair password
- [Betfair Application Key](https://docs.developer.betfair.com/display/1smk3cen4v3lu3yomq5qye0ni/Application+Keys)
- [Certificate Keys](https://docs.developer.betfair.com/display/1smk3cen4v3lu3yomq5qye0ni/Certificate+Generation+With+XCA)

```python
# Create an instance of the class with all the credentials & keys
betfair = PsusannxBetfair(
    username="<betfair-username>",
    password="<betfair-password>",
    app_key="<application-key",
    crt_path="<path-to-crt-key>",
    pem_path="<path-to-pem-key>".
    team_mapping={"team_name": "new_team_name"}
)
```

The `betfair` object can now be used to call the above functions and get **delayed (~3mins)** match odds on the exchange.

## list_upcoming_pl_matches function

```python
# Use the betfair_ex_conn to get the upcoming premier league matches listed on the betfair exchange
upcoming_matches_df = betfair.list_upcoming_pl_matches()

# Print out the next 5 matches, their ID's on the exchange and their kickoff times
upcoming_matches_df.head()
```

## get_betfair_exchange_odds function

```python
# Get the delayed exchange odds for an upcoming premier league match
match_odds_df = betfair.get_betfair_exchange_odds(
    home_team='<home-team>', 
    away_team='<away-team>'
)

# Lood at the odds dataframe
match_odds_df
```

If the \<home-team> Vs \<away-team> match isn't available to bet on on the betfair exchange then the function will return a dataframe with NA values for the odds.

## Notes

- The package is quite restricted in what it can do, but it only needs to do things that are required by the parent project so there won't be much development.
- A potential new feature to add to the package is the ability to get odds on matches that are not currently listed on the betfair exchange on runtime. This would require storing historical odds information in a public place.
- If you want to develop similar functions for other leagues/sports I highly recommend using the [API Demo Tools](https://docs.developer.betfair.com/display/1smk3cen4v3lu3yomq5qye0ni/API+Demo+Tools) for testing out & generating API requests in your browser. It is hard to navigate through requests output on your own, so these tools allow you to use an interface to find your selections, then you can go into developer tools in your browser and copy the exact request that generated the results from your browser and use it in your code.
