# Habit Tracker Generator

A browser-based editor (Korean UI) for making habit tracker inserts for system diaries and saving them as PDFs. Nothing to install.

**Open the editor:** https://mov-ie.github.io/habit-tracker-generator/

## What it makes

A habit tracker you use with the insert **turned sideways**. Days 1–31 run across the long edge of the page (171mm), and each habit gets its own row. One month per page.

## Features

- **Dated or undated:** a dated version with the year and weekdays printed, or an undated one with only 1–31 and a blank for the month.
- **Red days:** Sundays and Korean public holidays (including substitute holidays) are printed in red. Holidays are updated automatically every month (see below). You can also add your own dates.
- **Tracker layout:** number of habit rows, habit name column width, a total column, weekday labels (s m t / su mo / none), day lines (none / light / solid), a week divider before each Sunday, and weekend shading.
- **Pre-filled habits:** enter one habit per line and the same habits are printed on every month. Leave it empty for blank rows.
- **Fonts:** pick the main font (Futura by default) and a **separate font for habit names**. Font sizes and italics are adjustable.
- **Colors and lines:** line color (dark brown #5B4636 by default), line weight, text color, red-day color, Saturday color, and shading color.
- **Ring side:** choose whether the rings sit at the top (turn the diary clockwise) or at the bottom. On the back of each leaf, the wider ring margin automatically moves to the other edge.
- **Output:** save at insert size, or lay out several pages on A4 or A3 with crop marks, single- or double-sided.

## How to use

1. Open the page.
2. In the left panel, set the **year** (연도), **first month** (시작 월), and **last month** (끝 월).
3. Under **Tracker** (트래커), choose the number of habit rows and the layout, and type your habits if you like.
4. Adjust fonts, colors, and margins. The preview on the right updates instantly.
5. Choose the **output paper** (출력 용지):
   - **Insert size** (속지 크기): one page per month at the real size, 86×171mm.
   - **A4 / A3:** several pages per sheet. Three 86×171mm pages fit on a landscape A4 sheet.
6. Click **PDF로 저장 / 인쇄** (Save as PDF / Print) at the bottom, then choose **Save as PDF** in the print dialog.

Your settings are saved in the browser, so they're still there next time. Click **처음 설정으로 되돌리기** (Reset to defaults) to start over.

### Fonts

The default font is Futura. If your computer has Futura (Macs do), it's used; otherwise the similar free font Jost is used instead. Habit names are often in Korean, so pick a Korean font under **습관 이름 폰트** (Habit name font), such as Apple SD Gothic Neo, AppleMyungjo, or a Nanum font. For any other installed font, choose **직접 입력…** (Custom) and type its name.

## Automatic holiday updates

Holidays live in `holidays.json`, which the page reads when it opens.

- On the 1st of every month, **GitHub Actions** fetches holidays from last year through two years ahead using the *KASI Special Day Information* API (한국천문연구원 특일 정보) on the Korean Public Data Portal, and updates `holidays.json`. Substitute and temporary holidays are included once announced.
- Years the government hasn't announced yet keep their existing values and are filled in automatically on a later run.
- GitHub Actions is free for public repositories.
- The workflow re-enables itself on every run, so the schedule doesn't pause after 60 days without repository activity.

### One-time setup

1. On [data.go.kr](https://www.data.go.kr), search for **한국천문연구원_특일 정보** and apply for access. Once approved, your API key is shown on My Page (either the encoded or decoded key works).
2. In this repository, go to **Settings → Secrets and variables → Actions → New repository secret**. Name it `HOLIDAY_API_KEY` and paste the key as the value.
3. Go to the **Actions** tab, open **Update holidays**, and click **Run workflow** to run it once now. If it succeeds, you'll see a commit updating `holidays.json`.

Without a key, the update is simply skipped and the page keeps working with the holidays it already has. If you download the page and open it locally, it uses its built-in holiday list.

## Printing tips

**Print dialog settings**
- Set scale to **100% (actual size)**. "Fit to page" shrinks the insert.
- Set margins to **None**.
- Turn off **headers and footers**.
- Turn on **background graphics** so red days and shading keep their color.
- If the paper size isn't picked up automatically, try **Chrome**.

**Double-sided printing**
- With **double-sided** layout, each leaf gets two months back to back, e.g. January on the front and February on the back.
- Print portrait layouts with **flip on long edge** and landscape layouts with **flip on short edge**. The panel tells you which.

**Cutting and paper**
- Print one sheet first and check the size with a ruler.
- Crop marks show where to cut, just outside each page corner.
- Most printers can't print the outer 3–5mm. Enter that value as the **printer safe margin** so nothing gets cut off.

## See also

- [Monthly Generator](https://mov-ie.github.io/monthly-generator/): monthly inserts and A4 wall calendars in the same style.
