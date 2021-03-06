# Introduction
This the code from a private research project. The project's aim is to gather and analyze data from the German-language website [Chefkoch][chefkoch].

## Data Source
Data is gathered from the German-language cooking website [Chefkoch][chefkoch]. Note: As of mid-October 2016 the chefkoch.de website's [terms of use][agb] made no provision restricting scraping the website for information, so this is all perfectly legal.

Inspecting their [robots.txt][robots.txt] reveals that chefkoch wants to restrict crawling behavior for some sub-folders (awesome hint from [Scrapehero][scrapehero]). I don't have insight into their folder structure, so have to guess which parts they are restricting. Most things (e.g., photos, user-pictures etc.) are uninteresting. I'm guessing "produkte" is the products beings sold on the website (not the recipes being referred to as "products"). The only one that might be tricky is ```/user/``` because I do want some info on the users (experience level etc.).

In an old [discussion on API usage][chefkoch_api_discussion] a chefkoch admin says that "grabbing information and putting it on other platforms" is disallowed. It's unclear from the wording whether _each_ or _both_ of the two activities are disallowed, so I'm assuming it's _both_ (frankly because it suits me best and who cares if I gather data for research purposes anyway).

This [awesome guide][austwick] by Jason Austwick is a useful resource.

## Code

### Category pages
**Background**  
Recipe pages on [Chefkoch][chefkoch] are organized into seven overlapping [categories][categories]:
* Baking and sweets (Backen & Süßspeisen)
* Drinks (Getränke)
* Type of recipe (Menüart), e.g. starter or main course
* Regional cuisine (Regional)
* Seasonal recipes (Saisonal)
* Special recipes (Spezielles), e.g. baby food or camping
* Method of preparation (Zubereitungsarten), don't really understand this category

Categories comprise 12k-260k recipes. Links to the recipes are listed on batches of 30 on 'category-list-pages' (like [this][cat-example]).

`crawl_category_subpages.py`  
This script uses a list of the category syntax and a list of *user-defined* path preferences in `config/`. It downloads the HTML code of each category-list-page and and stores it to a local txt file.

The user-agents are curtesy of [willdrevo][user_agents].

**CAUTION**
* As of Nov 2016 there are ~27k category-list-pages (@30 recipes each), weighing in at 5GB
* Downloading took several hours (with a reasonably fast connection)

## Notes
* Need to check out [grequests][grequests] library for asynchronous requests.

---
[chefkoch]: http://www.chefkoch.de
[agb]: http://www.chefkoch.de/terms-of-use.phps
[categories]: http://www.chefkoch.de/rezepte/kategorien/
[cat-example]: http://www.chefkoch.de/rs/s0g61/Zubereitungsarten.html
[robots.txt]: https://www.scrapehero.com/how-to-prevent-getting-blacklisted-while-scraping/
[scrapehero]: https://www.scrapehero.com/how-to-prevent-getting-blacklisted-while-scraping/
[austwick]: http://jakeaustwick.me/python-web-scraping-resource/#prerequisites
[chefkoch_api_discussion]: http://www.chefkoch.de/forum/2,43,681438/api-chefkoch-de-frei-nutzbar.html
[grequests]: https://github.com/kennethreitz/grequests
[user-agents]: http://willdrevo.com/public/text/user_agents.txt 