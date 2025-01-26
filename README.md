# Web-Scraping-Tricks

### Collect Category
#### Problem:
intertwined and interconnected elements
#### solution
check parent of element
```python
from requests_html import HTMLSession, HTML
from bs4 import BeautifulSoup

sub_subcategory = HTMLSession()

r = sub_subcategory.get(f"https://medrar.sa/", )

soup = BeautifulSoup(r.text, 'html.parser')
categories_dict = {}
categories_id = {}
for main_category in soup.select('ul.main-menu>li[class="lg:hidden text-sm font-bold"]'):
    main_category_name =     main_category.select_one('span').get_text(strip=True)
    categories_dict[main_category_name] = {}
    categories_id[eval(main_category.attrs.get("id"))] = [main_category_name]
    for subcategory in main_category.select('ul>li[class="lg:hidden text-sm font-bold"]'):
        # Check parent subcategory is main_category (dirct parent)
        if subcategory.parent.parent != main_category:
            continue

        subcategory_name = subcategory.find('span').get_text(strip=True)
        categories_dict[main_category_name][subcategory_name] = []
        categories_id[eval(subcategory.attrs.get("id"))] = [main_category_name, subcategory_name]

        for sub_subcategory in subcategory.select('ul > li[class="lg:hidden text-sm font-bold"]'):
            # Check parent sub_subcategory is subcategory (dirct parent)
            if sub_subcategory.parent.parent != subcategory:
                continue

            sub_subcategory_name = sub_subcategory.find('span').get_text(strip=True)
            categories_dict[main_category_name][subcategory_name].append(sub_subcategory_name)
            categories_id[eval(sub_subcategory.attrs.get("id"))] = [main_category_name, subcategory_name, sub_subcategory_name]

```
<details>
  <summary>Output</summary>
    
```
{
   "لكزس":{
      "Lexus LX":[
         "أصلي"
      ],
      "Lexus RX":[
         "أصلي",
         "ياباني"
      ],
      "Lexus LS":[
         "أصلي",
         "ياباني",
         "denso",
         "DEPO"
      ],
      "Lexus GS":[
         "ياباني"
      ],
      "Lexus ES":[
         "أصلي",
         "تايوان",
         "ماليزي",
         "ياباني"
      ],
      "Lexus IS":[
         
      ]
   },
   "تويوتا":{
      "لاند كروزر":[
         "أصلي",
         "DENSO",
         "وطني",
         "ياباني",
         "DEPO",
         "صيني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي"
      ],
      "برادو":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "DEPO",
         "صيني",
         "تايلاندي",
         "تايوان",
         "اماراتي"
      ],
      "فورتشنر":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "DENSO",
         "وطني",
         "تايلاندي",
         "صيني",
         "تايوان",
         "انجليزي",
         "اماراتي"
      ],
      "هايلكس":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "DENSO",
         "وطني",
         "تايوان",
         "DEPO",
         "صيني",
         "وطني",
         "اردني",
         "انجليزي",
         "اماراتي",
         "شمعات واسطبات"
      ],
      "اف جي":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "صيني"
      ],
      "سكويا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايوان",
         "انجليزي",
         "DENSO",
         "وطني",
         "صيني"
      ],
      "انوفا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "DENSO",
         "وطني",
         "صيني"
      ],
      "ربع":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "DEPO",
         "صيني"
      ],
      "شاص":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "DEPO",
         "صيني"
      ],
      "راف فور":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "DEPO",
         "DENSO",
         "وطني"
      ],
      "افالون":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "صيني",
         "DENSO"
      ],
      "كامري":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "DEPO",
         "صيني",
         "وطني"
      ],
      "كورولا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "صيني",
         "وطني"
      ],
      "يارس":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "DEPO",
         "صيني",
         "وطني"
      ],
      "هايس":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "DEPO",
         "صيني"
      ],
      "افانزا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايوان",
         "انجليزي",
         "اماراتي",
         "DEPO",
         "صيني"
      ],
      "بريفيا":[
         "أصلي",
         "ياباني",
         "تايلاندي",
         "انجليزي"
      ],
      "ايكو":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "صيني"
      ],
      "اوريون":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "تايوان",
         "انجليزي",
         "DEPO",
         "صيني"
      ],
      "كرسيدا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايوان",
         "DEPO"
      ]
   },
   "ميتسوبيشي":{
      "باجيرو":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني",
         "تايوان",
         "إماراتي"
      ],
      "مونتيرو":[
         "أصلي",
         "ياباني"
      ],
      "سبيس واجن":[
         "أصلي",
         "ياباني",
         "صيني",
         "تايوان"
      ],
      "وانيت":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني",
         "تايوان",
         "إماراتي",
         "تجاري",
         "DEPO"
      ],
      "لانسر":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني",
         "تايوان",
         "إماراتي",
         "تجاري"
      ],
      "ستار":[
         "أصلي"
      ],
      "اوتلاندر":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "صيني"
      ],
      "اكليبس":[
         "أصلي"
      ],
      "كنتر":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني",
         "تايوان",
         "تجاري"
      ],
      "ناتيفا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني"
      ],
      "باص روزا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني",
         "تايوان"
      ],
      "اكسباندر":[
         "تايلاندي"
      ],
      "اتراج":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني",
         "تايوان",
         "إماراتي",
         "تجاري"
      ],
      "جلنت":[
         "ياباني",
         "ماليزي"
      ],
      "جرانديز":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "تايلاندي",
         "صيني",
         "تايوان",
         "KO KO"
      ]
   },
   "نيسان":{
      "باترول":[
         "أصلي",
         "تايلندي",
         "ياباني",
         "ماليزي",
         "صيني",
         "انجليزي"
      ],
      "اكس تريل":[
         "أصلي",
         "ياباني",
         "اماراتي",
         "انجليزي"
      ],
      "ماكسيما":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "اماراتي",
         "صيني",
         "انجليزي"
      ],
      "التيما":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "اماراتي",
         "صيني",
         "انجليزي"
      ],
      "تيدا":[
         "ياباني",
         "انجليزي"
      ],
      "بيك آب ددسن":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "صيني",
         "انجليزي",
         "تايلندي"
      ],
      "صني":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "اماراتي",
         "صيني",
         "انجليزي",
         "تايلندي"
      ],
      "باثفايندر":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "اماراتي",
         "صيني",
         "انجليزي",
         "تايلندي"
      ],
      "انفنتي":[
         "أصلي",
         "ياباني",
         "ماليزي"
      ],
      "اكس تيرا":[
         "أصلي",
         "ياباني"
      ],
      "كيكس":[
         "أصلي",
         "ياباني"
      ],
      "اورفان":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "انجليزي",
         "تايلندي"
      ],
      "نافارا":[
         "أصلي",
         "ياباني",
         "صيني"
      ],
      "سنترا":[
         "أصلي",
         "ياباني"
      ],
      "ارمادا":[
         "أصلي",
         "ياباني",
         "ماليزي",
         "اماراتي",
         "انجليزي"
      ]
   },
   "ايسوزو":{
      "دينا ايسوزو":[
         "أصلي",
         "ياباني",
         "تايوان",
         "صيني",
         "تايلاندي",
         "تجاري"
      ],
      "ونيت ايسوزو":[
         "أصلي",
         "ياباني",
         "تايوان",
         "صيني",
         "تايلاندي",
         "تجاري"
      ],
      "ديمكس ايسوزو":[
         "أصلي",
         "ياباني",
         "تايوان",
         "صيني",
         "إماراتي",
         "تايلاندي",
         "تجاري"
      ],
      "اسطبات وشمعات ايسوزو":[
         
      ]
   }
}
```
</details>

### nodriver/zendriver

#### wait_for_element
```python
async def wait_for_element(page, selector, timeout=30000):
    try:
        element = await page.wait_for(selector, timeout=timeout)
        return element
    except asyncio.TimeoutError:
        raise Exception(f"Timeout waiting for element: {selector}")
    except Exception as e:
        raise Exception(f"Error finding element {selector}: {str(e)}")
```

#### listen to requests
```python
        await page.evaluate("""
            window.requests = [];
            const originalFetch = window.fetch;
            window.fetch = function() {
                return new Promise((resolve, reject) => {
                    originalFetch.apply(this, arguments)
                        .then(response => {
                            window.requests.push({
                                url: response.url,
                                status: response.status,
                                headers: Object.fromEntries(response.headers.entries())
                            });
                            resolve(response);
                        })
                        .catch(reject);
                });
            };
        """)
```

#### check requests

```python
async def wait_for_token(page, max_attempts=10, check_interval=0.5):
    for _ in range(max_attempts):
        requests = await page.evaluate("window.requests")
        for req in requests:
            if "api.spotifydown.com/download" in req['url']:
                token_match = re.search(r'token=(.+)$', req['url'])
                if token_match:
                    return token_match.group(1)
        await asyncio.sleep(check_interval)
    raise Exception("Token not found within timeout period")

page = await browser.get("https://spotifydown.com/en")
```

#### request status code
```python
    page = await browser.get("https://httpstat.us/404")
    status_code: int = await page.evaluate(
        'window.performance.getEntries().find(e => e.entryType === "navigation").responseStatus'
    )
    print(status_code)  # 404
```

#### request, response listen

```python
import asyncio
import zendriver as zd

async def request_handler(event: zd.cdp.network.RequestWillBeSent):
    print(f"Request URL: {event.request.url}")
    print(f"Method: {event.request.method}")
    print(f"Headers: {event.request.headers}")

async def response_handler(event: zd.cdp.network.ResponseReceived):
    print(f"Response URL: {event.response.url}")
    print(f"Status: {event.response.status}")
    print(f"Headers: {event.response.headers}")

async def main():
        async with await zd.start(
                headless=False,
        ) as browser:
            page = await browser.get()

            page.add_handler(zd.cdp.network.RequestWillBeSent, request_handler)
            page.add_handler(zd.cdp.network.ResponseReceived, response_handler)

            await page.get(f'https://translate.google.com/')
            await page.get(f'https://translate.google.com/?hl=ar&eotf=0&sl=auto&tl=ar&op=images')


asyncio.run(main())
```
