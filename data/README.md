# Facebook Posts Data

## Source
Facebook data export — downloaded from Google Drive (avizmaeir@gmail.com).

## Drive File IDs

| File | Drive ID | Posts |
|------|----------|-------|
| `your_posts__check_ins__photos_and_videos_1.json` | `1UhV7m_BqrJhwqB4pX7AP6O5RTuEYZiIa` | 10,000 (2009–2026) |
| `your_posts__check_ins__photos_and_videos_2.json` | `1sUTww32wOGBtKp7AP6O5RTuEYZiIa` | TBD |
| `your_posts__check_ins__photos_and_videos_3.json` | `14N0MNUSCMGGXYZG-5_bYtKMUpFcVBWMm` | TBD |

## Download

```bash
~/.cargo/bin/gws drive files get \
  --params '{"fileId": "1UhV7m_BqrJhwqB4pX7AP6O5RTuEYZiIa", "alt": "media"}' \
  > /tmp/fb_posts_1.json
```

## Encoding Fix (Hebrew Mojibake)

Facebook export JSONs are triple-encoded. Hebrew appears as `Ã\x97Â¤...`.

```python
def fix(s):
    try:
        b = s.encode('latin-1')
        mid = b.decode('utf-8')
        return mid.encode('latin-1').decode('utf-8')
    except:
        try:
            return s.encode('latin-1').decode('utf-8')
        except:
            return s
```

## Data Structure

```json
{
  "timestamp": 1419993120,
  "title": "Avraham Yitzchak Maeir...",
  "data": [{"post": "ENCODED_HEBREW_TEXT"}],
  "attachments": [{"data": [...]}]
}
```

**Important:** No post IDs or direct URLs in the export.

## Search Example

```python
import json, datetime

def fix(s):
    try:
        return s.encode('latin-1').decode('utf-8').encode('latin-1').decode('utf-8')
    except:
        return s

data = open('/tmp/fb_posts_1.json', 'rb').read().decode('latin-1')
posts = json.loads(data)

for p in posts:
    if p.get('data'):
        for d in p['data']:
            if 'post' in d:
                text = fix(d['post'])
                if 'רוטשילד' in text:
                    dt = datetime.datetime.fromtimestamp(p['timestamp'])
                    print(dt, text[:200])
```

## Key Biographical Posts

See `posts-lookup.json` for timestamps of landmark posts (memoir, 2015 crisis, Rothschild/Tisha B'Av).
