<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Italy + Zurich Travel Guide</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
  <style>
    :root {
      --ink:     #1a1a1a;
      --muted:   #6b6b6b;
      --rule:    #e8e3dc;
      --accent:  #c0392b;
      --gold:    #b8860b;
      --cream:   #faf8f4;
      --card-bg: #ffffff;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background: #ede9e1;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      padding: 28px 16px 48px;
      font-family: 'DM Sans', sans-serif;
    }

    /* ── Outer shell ── */
    .book {
      width: 100%;
      max-width: 440px;
      background: var(--cream);
      border-radius: 18px;
      overflow: hidden;
      box-shadow:
        0 2px 0 rgba(0,0,0,.06),
        0 8px 32px rgba(0,0,0,.14),
        0 24px 64px rgba(0,0,0,.08);
      position: relative;
    }

    /* ── Sticky top bar ── */
    .top-bar {
      position: sticky;
      top: 0;
      z-index: 20;
      background: var(--cream);
      border-bottom: 1px solid var(--rule);
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px 20px 12px;
    }
    .top-bar .trip-label {
      font-family: 'Playfair Display', serif;
      font-size: 13px;
      letter-spacing: .08em;
      color: var(--muted);
      text-transform: uppercase;
    }
    .progress-dots {
      display: flex;
      gap: 5px;
    }
    .dot {
      width: 6px; height: 6px;
      border-radius: 50%;
      background: var(--rule);
      transition: background .25s;
    }
    .dot.active { background: var(--accent); }
    .dot.visited { background: var(--gold); opacity: .55; }

    /* ── Page ── */
    .page {
      display: none;
      padding: 0 0 100px;   /* bottom pad for nav */
      min-height: calc(100vh - 120px);
    }
    .page.active { display: block; }

    /* ── Hero band ── */
    .page-hero {
      width: 100%;
      height: 200px;
      position: relative;
      overflow: hidden;
    }
    .page-hero img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }
    .page-hero-overlay {
      position: absolute;
      inset: 0;
      background: linear-gradient(to bottom, rgba(0,0,0,.08) 0%, rgba(0,0,0,.55) 100%);
    }
    .page-hero-text {
      position: absolute;
      bottom: 18px;
      left: 22px;
      right: 22px;
      color: #fff;
    }
    .page-hero-text h2 {
      font-family: 'Playfair Display', serif;
      font-size: 26px;
      line-height: 1.2;
      margin-bottom: 4px;
    }
    .page-hero-text .sub {
      font-size: 12px;
      opacity: .85;
      letter-spacing: .05em;
      text-transform: uppercase;
    }
    .page-hero-text .accommodation {
      font-size: 12px;
      opacity: .75;
      margin-top: 2px;
    }

    /* ── Body content ── */
    .page-body {
      padding: 24px 20px 0;
    }

    /* ── Activity card ── */
    .activity {
      margin-bottom: 28px;
    }
    .activity-img-wrap {
      width: 100%;
      height: 190px;
      border-radius: 12px;
      overflow: hidden;
      margin-bottom: 14px;
      position: relative;
    }
    .activity-img-wrap img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      transition: transform .4s ease;
    }
    .activity:hover .activity-img-wrap img { transform: scale(1.03); }
    .activity-img-wrap .time-badge {
      position: absolute;
      top: 10px; left: 10px;
      background: rgba(26,26,26,.72);
      backdrop-filter: blur(6px);
      color: #fff;
      font-size: 11px;
      font-weight: 500;
      letter-spacing: .06em;
      padding: 4px 9px;
      border-radius: 20px;
      text-transform: uppercase;
    }

    .activity-tag {
      display: inline-block;
      font-size: 10px;
      font-weight: 500;
      letter-spacing: .1em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 5px;
    }
    .activity h3 {
      font-family: 'Playfair Display', serif;
      font-size: 19px;
      color: var(--ink);
      margin-bottom: 4px;
      line-height: 1.3;
    }
    .activity-punchline {
      font-size: 13px;
      font-weight: 500;
      color: var(--gold);
      margin-bottom: 8px;
      line-height: 1.4;
      font-style: italic;
    }
    .activity-desc {
      font-size: 14px;
      color: #555;
      line-height: 1.7;
    }

    /* ── Divider ── */
    .divider {
      height: 1px;
      background: var(--rule);
      margin: 0 0 28px;
    }

    /* ── Tip box ── */
    .tip-box {
      background: #fff8ec;
      border-left: 3px solid var(--gold);
      border-radius: 0 8px 8px 0;
      padding: 12px 14px;
      margin-bottom: 28px;
      font-size: 13px;
      color: #5a4a1e;
      line-height: 1.6;
    }
    .tip-box strong { font-weight: 600; }

    /* ── Bottom nav ── */
    .bottom-nav {
      position: sticky;
      bottom: 0;
      left: 0; right: 0;
      background: var(--cream);
      border-top: 1px solid var(--rule);
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px 20px;
      gap: 12px;
    }
    .nav-btn {
      padding: 10px 22px;
      background: var(--ink);
      color: #fff;
      border: none;
      border-radius: 8px;
      font-family: 'DM Sans', sans-serif;
      font-size: 13px;
      font-weight: 500;
      cursor: pointer;
      transition: opacity .2s, transform .1s;
      letter-spacing: .03em;
    }
    .nav-btn:active { transform: scale(.97); }
    .nav-btn:disabled { background: #ccc; cursor: not-allowed; }
    .day-counter {
      font-size: 12px;
      color: var(--muted);
      letter-spacing: .05em;
      text-align: center;
      flex: 1;
    }
  </style>
</head>
<body>

<div class="book">

  <!-- Sticky top bar with progress dots -->
  <div class="top-bar">
    <span class="trip-label">Italy + Zurich</span>
    <div class="progress-dots" id="dots"></div>
  </div>

  <!-- ============================================================
       DAY 1
  ============================================================ -->
  <div class="page active" id="page1">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1544928147-79a2dbc1f389?w=800&q=80" alt="Zurich" onerror="this.src='https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 1 — Saturday</h2>
        <div class="sub">Zurich → Milan</div>
        <div class="accommodation">🏨 Accommodation: Milan</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1566438480900-0609be27a4be?w=800&q=80" alt="Zurich Airport" onerror="this.src='https://images.unsplash.com/photo-1436491865332-7a61a109cc05?w=800&q=80'" />
          <span class="time-badge">10:30</span>
        </div>
        <div class="activity-tag">Arrival</div>
        <h3>Zurich Airport</h3>
        <div class="activity-punchline">"One of Europe's slickest airports—you'll actually enjoy it."</div>
        <div class="activity-desc">Land at 10:30 and clear one of Europe's most efficient airports. Expect to be through immigration and at the baggage carousel within 40 minutes. Zurich Airport is immaculate, well-signed, and stress-free—a perfect entry to Switzerland.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1548345680-f5475ea5df84?w=800&q=80" alt="Zurich Old Town" onerror="this.src='https://images.unsplash.com/photo-1560948799-dc6e6c7b9b58?w=800&q=80'" />
          <span class="time-badge">11:20 – 15:00</span>
        </div>
        <div class="activity-tag">City Walk</div>
        <h3>Zurich City Layover</h3>
        <div class="activity-punchline">"Swiss precision meets lakeside beauty—a city that earns every cliché."</div>
        <div class="activity-desc">Hop the direct train to Zurich HB in 10 minutes. Stroll the Bahnhofstrasse—Europe's most expensive shopping street—then walk the Limmat River into the Altstadt (Old Town). The twin-towered Grossmünster and the colourful Fraumünster are worth a quick peek. End at Lake Zurich for a coffee with a view before heading back.</div>
      </div>

      <div class="tip-box">
        <strong>💡 Local Tip:</strong> The Zurich Card (24h) covers all transit from the airport plus free museum entry. Worth it for a half-day stop.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1528360983277-13d401cdc186?w=800&q=80" alt="Swiss Train" onerror="this.src='https://images.unsplash.com/photo-1474487548417-781cb71495f3?w=800&q=80'" />
          <span class="time-badge">15:30</span>
        </div>
        <div class="activity-tag">Transfer</div>
        <h3>Train to Milan (SBB/Trenitalia)</h3>
        <div class="activity-punchline">"Crossing the Alps by rail is a travel highlight in itself."</div>
        <div class="activity-desc">The 15:30 direct IC from Zurich HB to Milano Centrale (3h 35m) threads through the Gotthard Base Tunnel—the world's longest railway tunnel—and descends into Italy's Po Valley. Arrive ~19:05, drop bags, and catch the Duomo illuminated at night. Book in advance on SBB.ch for best prices.</div>
      </div>

    </div><!-- /page-body -->

    <div class="bottom-nav">
      <button class="nav-btn" disabled>← Prev</button>
      <span class="day-counter" id="counter1">Day 1 of 9</span>
      <button class="nav-btn" onclick="goTo(2)">Next →</button>
    </div>
  </div><!-- /page1 -->

  <!-- ============================================================
       DAY 2
  ============================================================ -->
  <div class="page" id="page2">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1520175480921-4edfa2983e0f?w=800&q=80" alt="Milan Duomo" onerror="this.src='https://images.unsplash.com/photo-1513581166391-887a96ddeafd?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 2 — Sunday</h2>
        <div class="sub">Milan</div>
        <div class="accommodation">🏨 Accommodation: Milan</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1548438294-1ad5d5f4f063?w=800&q=80" alt="Last Supper" onerror="this.src='https://images.unsplash.com/photo-1567448400815-bff7b62ace54?w=800&q=80'" />
          <span class="time-badge">09:30</span>
        </div>
        <div class="activity-tag">Must-See Art</div>
        <h3>The Last Supper</h3>
        <div class="activity-punchline">"15 minutes with Leonardo—and every second will stay with you forever."</div>
        <div class="activity-desc">Leonardo da Vinci's <em>Il Cenacolo</em> is housed in the refectory of Santa Maria delle Grazie. Visits are tightly controlled: maximum 30 people at a time, 15 minutes inside. The experience is hushed, nearly sacred. Book online months in advance—this cannot be bought on the door. Arrive 15 minutes early; late entry is refused.</div>
      </div>

      <div class="tip-box">
        <strong>⚠️ Book ahead:</strong> vivaticket.com or museicivicimilano.cultura.toscana.it. Tickets sell out 2–3 months in advance for peak season.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1582560475093-ba66accbc424?w=800&q=80" alt="Sforza Castle" onerror="this.src='https://images.unsplash.com/photo-1530789253388-582c481c54b0?w=800&q=80'" />
          <span class="time-badge">11:30</span>
        </div>
        <div class="activity-tag">History</div>
        <h3>Sforza Castle (Castello Sforzesco)</h3>
        <div class="activity-punchline">"A fortress that shaped the Renaissance—and holds a Michelangelo most people miss."</div>
        <div class="activity-desc">Built in the 15th century by Francesco Sforza, this massive red-brick castle was once one of the largest in Europe. Inside, seven civic museums house Egyptian antiquities, Renaissance furniture, and—crucially—Michelangelo's unfinished <em>Pietà Rondanini</em>, his final sculpture before his death. The park behind it (Parco Sempione) is great for a picnic.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1516483638261-f4dbaf036963?w=800&q=80" alt="Milan Duomo rooftop" onerror="this.src='https://images.unsplash.com/photo-1515542622106-78bda8ba0e5b?w=800&q=80'" />
          <span class="time-badge">14:30</span>
        </div>
        <div class="activity-tag">Icon</div>
        <h3>Duomo & Galleria Vittorio Emanuele II</h3>
        <div class="activity-punchline">"Walk the rooftop spires at sunset—Milan's skyline belongs to you."</div>
        <div class="activity-desc">The Duomo di Milano took nearly 600 years to complete and bristles with 3,400 statues and 135 spires. Take the elevator to the rooftop and wander among the marble pinnacles with views across Lombardy on clear days. Afterwards, duck into the Galleria—Italy's oldest active shopping mall (1877), a glass-vaulted arcade with Prada, Louis Vuitton, and the legendary Caffè Biffi.</div>
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(1)">← Prev</button>
      <span class="day-counter">Day 2 of 9</span>
      <button class="nav-btn" onclick="goTo(3)">Next →</button>
    </div>
  </div><!-- /page2 -->

  <!-- ============================================================
       DAY 3
  ============================================================ -->
  <div class="page" id="page3">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1514890547357-a9ee288728e0?w=800&q=80" alt="Venice canals" onerror="this.src='https://images.unsplash.com/photo-1534113414509-0eec2bfb493f?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 3 — Monday</h2>
        <div class="sub">Milan → Venice</div>
        <div class="accommodation">🏨 Accommodation: Venice</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1474487548417-781cb71495f3?w=800&q=80" alt="High speed train Italy" onerror="this.src='https://images.unsplash.com/photo-1532105956626-9569c03602f6?w=800&q=80'" />
          <span class="time-badge">08:30</span>
        </div>
        <div class="activity-tag">Transfer</div>
        <h3>High-Speed Train to Venice</h3>
        <div class="activity-punchline">"The train pulls into a lagoon. No roads. Pure magic from the first second."</div>
        <div class="activity-desc">Trenitalia Frecciarossa from Milano Centrale to Venezia Santa Lucia (2h 25m). The final approach is unforgettable—the rail bridge crosses open water for 4km, and you step off the train directly onto the banks of the Grand Canal. No cars, no roads, no noise. Just boats and bridges.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1533104816931-20fa691ff6ca?w=800&q=80" alt="Venice St Mark's Square" onerror="this.src='https://images.unsplash.com/photo-1513622470522-26c3c8a854bc?w=800&q=80'" />
          <span class="time-badge">11:30 – 17:00</span>
        </div>
        <div class="activity-tag">Explore</div>
        <h3>St. Mark's, Doge's Palace & Rialto</h3>
        <div class="activity-punchline">"Get lost on purpose—the best Venice moments happen when you stop following a map."</div>
        <div class="activity-desc">Start at Piazza San Marco, Napoleon's "drawing room of Europe." Visit the Byzantine mosaic interior of the Basilica (free; bag drop required). Queue early for the Doge's Palace to walk the <em>Bridge of Sighs</em>. Then cross the Rialto Bridge and dive into the warren of <em>sestieri</em>—each turn reveals a new canal, a hidden campo, a tiny bacaro (wine bar). Eat cicchetti (Venetian tapas) with Spritz Aperol for lunch.</div>
      </div>

      <div class="tip-box">
        <strong>💡 Avoid the crowds:</strong> St. Mark's is mobbed 10am–3pm. Go before 9am or after 5pm for a dramatically quieter experience.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1534430480872-3498386e7856?w=800&q=80" alt="Venice sunset" onerror="this.src='https://images.unsplash.com/photo-1513805959324-96eb66ca8713?w=800&q=80'" />
          <span class="time-badge">18:00</span>
        </div>
        <div class="activity-tag">Golden Hour</div>
        <h3>Sunset on the Lagoon</h3>
        <div class="activity-punchline">"Venice turns to copper at dusk. Find a quiet fondamenta and just sit."</div>
        <div class="activity-desc">Walk to the Zattere promenade on the Giudecca Canal for the best sunset views—wide water, no crowds, and the domes of Il Redentore glowing across the channel. Then dinner in Dorsoduro, away from the tourist crush: try <em>sarde in saor</em> (sweet-sour sardines) or fresh lagoon shrimp at a family trattoria.</div>
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(2)">← Prev</button>
      <span class="day-counter">Day 3 of 9</span>
      <button class="nav-btn" onclick="goTo(4)">Next →</button>
    </div>
  </div><!-- /page3 -->

  <!-- ============================================================
       DAY 4
  ============================================================ -->
  <div class="page" id="page4">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&q=80" alt="Burano colorful houses" onerror="this.src='https://images.unsplash.com/photo-1504609813442-a8924e83f76e?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 4 — Tuesday</h2>
        <div class="sub">Venice Islands Day Trip</div>
        <div class="accommodation">🏨 Accommodation: Venice</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1566408669374-5a6d5dca1ef5?w=800&q=80" alt="Burano island" onerror="this.src='https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&q=80'" />
          <span class="time-badge">09:00</span>
        </div>
        <div class="activity-tag">Island Escape</div>
        <h3>Burano</h3>
        <div class="activity-punchline">"The most photogenic place in Italy—and the pasta is even better than the views."</div>
        <div class="activity-desc">Take Vaporetto Line 12 from Fondamente Nove (~40 mins). Burano is a fishing island where every house is painted a different bold colour—by law, neighbours cannot share the same shade. The colour tradition supposedly helped fishermen spot their homes through the lagoon fog. Try a <em>bussolà</em> (ring-shaped butter cookie) from a local bakery and browse the lace-work shops. Walk every canal—the island is tiny but endlessly photogenic.</div>
      </div>

      <div class="tip-box">
        <strong>💡 Timing:</strong> Arrive by 9:30am before the day-tripper boats arrive around 11am. The island is genuinely quiet in the morning.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1516483638261-f4dbaf036963?w=800&q=80" alt="Torcello cathedral" onerror="this.src='https://images.unsplash.com/photo-1530789253388-582c481c54b0?w=800&q=80'" />
          <span class="time-badge">13:30</span>
        </div>
        <div class="activity-tag">Ancient History</div>
        <h3>Torcello Island</h3>
        <div class="activity-punchline">"The island that was Venice before Venice existed—hauntingly, beautifully empty."</div>
        <div class="activity-desc">Once the most populous island in the lagoon (10,000+ inhabitants in the 10th century), Torcello is now home to fewer than 20 people and an extraordinary 7th-century cathedral. The Cathedral of Santa Maria Assunta contains some of the finest Byzantine mosaics in Europe—the <em>Last Judgment</em> mosaic on the west wall is breathtaking. Sit on the Throne of Attila (a stone chair in the square) for luck.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1523906834658-6e24ef2386f9?w=800&q=80" alt="Venice Grand Canal night" onerror="this.src='https://images.unsplash.com/photo-1534113414509-0eec2bfb493f?w=800&q=80'" />
          <span class="time-badge">17:30</span>
        </div>
        <div class="activity-tag">Evening</div>
        <h3>Venice by Night</h3>
        <div class="activity-punchline">"When the day-trippers leave, Venice becomes yours."</div>
        <div class="activity-desc">Return to the main island by 17:30. As evening falls, Venice transforms—the tour groups thin, the light turns amber, and the reflections on the canals come alive. Stroll across the Accademia Bridge for Grand Canal views, then wind through the Cannaregio sestiere to find a quiet bacaro for ombra (small glass of wine) and cichetti before dinner.</div>
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(3)">← Prev</button>
      <span class="day-counter">Day 4 of 9</span>
      <button class="nav-btn" onclick="goTo(5)">Next →</button>
    </div>
  </div><!-- /page4 -->

  <!-- ============================================================
       DAY 5
  ============================================================ -->
  <div class="page" id="page5">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1541370976299-4d24be63c5c1?w=800&q=80" alt="Florence Duomo" onerror="this.src='https://images.unsplash.com/photo-1467269204594-9661b134dd2b?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 5 — Wednesday</h2>
        <div class="sub">Venice → Florence</div>
        <div class="accommodation">🏨 Accommodation: Florence</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1502602898657-3e91760cbb34?w=800&q=80" alt="Italian train" onerror="this.src='https://images.unsplash.com/photo-1474487548417-781cb71495f3?w=800&q=80'" />
          <span class="time-badge">08:00</span>
        </div>
        <div class="activity-tag">Transfer</div>
        <h3>Train to Florence</h3>
        <div class="activity-punchline">"Two hours, and you travel from watery Gothic to golden Renaissance."</div>
        <div class="activity-desc">Frecciarossa Venice → Florence Santa Maria Novella, ~2 hours. Arrive by 10:00, check into your hotel, and walk out into Brunelleschi's dome dominating the skyline. Florence is compact and largely walkable—most major sites are within 15 minutes of each other.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1467269204594-9661b134dd2b?w=800&q=80" alt="Florence Duomo dome" onerror="this.src='https://images.unsplash.com/photo-1541370976299-4d24be63c5c1?w=800&q=80'" />
          <span class="time-badge">11:00</span>
        </div>
        <div class="activity-tag">Architecture</div>
        <h3>Duomo Climb & Ponte Vecchio</h3>
        <div class="activity-punchline">"Climbing inside Brunelleschi's dome is like walking through engineering genius."</div>
        <div class="activity-desc">Filippo Brunelleschi's dome (1436) was the largest built since the Pantheon and remains a feat of engineering—he invented his own hoisting machines to build it. The 463-step climb winds between the inner and outer shell, with a peek at the fresco-covered interior before emerging on the lantern with 360° views of Tuscany. Then walk south to the Ponte Vecchio—the only Florentine bridge the retreating Nazis refused to destroy in 1944.</div>
      </div>

      <div class="tip-box">
        <strong>💡 Book ahead:</strong> The Duomo climb requires timed-entry tickets via operaduomo.firenze.it. Morning slots fill up fast.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1578301978162-7aae4d755744?w=800&q=80" alt="Uffizi Gallery Florence" onerror="this.src='https://images.unsplash.com/photo-1534430480872-3498386e7856?w=800&q=80'" />
          <span class="time-badge">15:00</span>
        </div>
        <div class="activity-tag">World-Class Art</div>
        <h3>Uffizi Gallery</h3>
        <div class="activity-punchline">"Room 10: Botticelli's Birth of Venus will actually stop you in your tracks."</div>
        <div class="activity-desc">The Uffizi is arguably the world's greatest repository of Renaissance painting. Built in 1560 as the Medici's administrative offices, it has housed their art collection since 1581. Botticelli's <em>Birth of Venus</em> and <em>Primavera</em>, Leonardo's <em>Annunciation</em>, Caravaggio, Raphael, Michelangelo—plan 2–3 hours minimum. Don't try to see everything; pick a few rooms and look deeply. Book tickets online to skip the queues.</div>
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(4)">← Prev</button>
      <span class="day-counter">Day 5 of 9</span>
      <button class="nav-btn" onclick="goTo(6)">Next →</button>
    </div>
  </div><!-- /page5 -->

  <!-- ============================================================
       DAY 6
  ============================================================ -->
  <div class="page" id="page6">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1552832230-c0197dd311b5?w=800&q=80" alt="Tuscany hills" onerror="this.src='https://images.unsplash.com/photo-1467190899367-2db2d666fdad?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 6 — Thursday</h2>
        <div class="sub">Tuscany Day Trip</div>
        <div class="accommodation">🏨 Accommodation: Florence</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1509439581779-6298f75bf6e5?w=800&q=80" alt="Siena Piazza del Campo" onerror="this.src='https://images.unsplash.com/photo-1552832230-c0197dd311b5?w=800&q=80'" />
          <span class="time-badge">09:00</span>
        </div>
        <div class="activity-tag">Medieval City</div>
        <h3>Siena</h3>
        <div class="activity-punchline">"Better preserved than Rome, less crowded than Florence—Siena is Tuscany's best-kept secret."</div>
        <div class="activity-desc">Bus from Florence SITA Nord terminal (1h 15m, €8). The heart of Siena is the shell-shaped Piazza del Campo—home to the famous Palio horse race twice a year and simply one of the most beautiful medieval squares in existence. Climb the Torre del Mangia for panoramic views, then visit the black-and-white striped Gothic Duomo. Don't leave without tasting <em>ricciarelli</em> (almond paste biscuits) or a glass of Chianti Classico.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1534430480872-3498386e7856?w=800&q=80" alt="San Gimignano towers" onerror="this.src='https://images.unsplash.com/photo-1467190899367-2db2d666fdad?w=800&q=80'" />
          <span class="time-badge">14:30</span>
        </div>
        <div class="activity-tag">Medieval Towers</div>
        <h3>San Gimignano</h3>
        <div class="activity-punchline">"Manhattan, 800 years earlier—a skyline of stone towers over rolling Tuscan hills."</div>
        <div class="activity-desc">A short bus from Siena brings you to San Gimignano, a UNESCO World Heritage hilltop town famous for its 14 surviving medieval towers (once there were 72). Wealthy rival families competed by building taller towers as symbols of power—an early arms race in stone. Climb the Torre Grossa for sweeping Chianti valley views. Buy a bottle of Vernaccia di San Gimignano (Italy's first DOC white wine) to take home.</div>
      </div>

      <div class="tip-box">
        <strong>🍷 Gelato alert:</strong> Gelateria Dondoli on Piazza della Cisterna has won the World Gelato Championship. The Saffron & Pine Nut flavour is extraordinary.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1516483638261-f4dbaf036963?w=800&q=80" alt="Florence evening Arno" onerror="this.src='https://images.unsplash.com/photo-1541370976299-4d24be63c5c1?w=800&q=80'" />
          <span class="time-badge">18:30</span>
        </div>
        <div class="activity-tag">Evening Return</div>
        <h3>Back to Florence for Dinner</h3>
        <div class="activity-punchline">"Bistecca alla Fiorentina: a 1kg T-bone cooked over wood fire, medium rare, no negotiation."</div>
        <div class="activity-desc">Return to Florence by bus/train. Walk the Arno embankment at golden hour—the view of Ponte Vecchio from Ponte Santa Trinita is one of Italy's finest photo opportunities. Dinner tonight calls for the iconic <em>Bistecca alla Fiorentina</em>—the T-bone Florentines take deadly seriously: always from Chianina cattle, always rare, always enormous. Pair with a glass of Brunello di Montalcino.</div>
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(5)">← Prev</button>
      <span class="day-counter">Day 6 of 9</span>
      <button class="nav-btn" onclick="goTo(7)">Next →</button>
    </div>
  </div><!-- /page6 -->

  <!-- ============================================================
       DAY 7
  ============================================================ -->
  <div class="page" id="page7">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1552465011-b4e21bf6e79a?w=800&q=80" alt="Rome Colosseum" onerror="this.src='https://images.unsplash.com/photo-1515542622106-78bda8ba0e5b?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 7 — Friday</h2>
        <div class="sub">Florence → Rome</div>
        <div class="accommodation">🏨 Accommodation: Rome</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1474487548417-781cb71495f3?w=800&q=80" alt="Italian train" onerror="this.src='https://images.unsplash.com/photo-1502602898657-3e91760cbb34?w=800&q=80'" />
          <span class="time-badge">08:30</span>
        </div>
        <div class="activity-tag">Transfer</div>
        <h3>Train to Rome</h3>
        <div class="activity-punchline">"90 minutes from the Renaissance to the Roman Empire."</div>
        <div class="activity-desc">Frecciarossa Florence SMN → Roma Termini (1h 30m). Arrive by 10:00, check in, and prepare for two days in the Eternal City. Rome's layers are unique: a papal baroque city wrapped around a medieval city built on top of an ancient one. The history is literally underground—and above, and everywhere.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1552465011-b4e21bf6e79a?w=800&q=80" alt="Colosseum Rome" onerror="this.src='https://images.unsplash.com/photo-1513581166391-887a96ddeafd?w=800&q=80'" />
          <span class="time-badge">11:30</span>
        </div>
        <div class="activity-tag">Ancient Rome</div>
        <h3>Colosseum & Roman Forum</h3>
        <div class="activity-punchline">"Stand where 50,000 Romans cheered. History isn't abstract here—it's under your feet."</div>
        <div class="activity-desc">The Colosseum (72 AD) held up to 80,000 spectators for gladiatorial contests, animal hunts, and executions. Buy a combined ticket that also covers the Roman Forum and Palatine Hill. The Forum was the centre of Roman public life for centuries—walk along the Sacred Way past temples, arches, and basilicas. Allow 3 hours for all three sites. Book online; the physical queue can be 2 hours long.</div>
      </div>

      <div class="tip-box">
        <strong>💡 Best photo spot:</strong> The Colosseum from Via Sacra inside the Forum, with the Arch of Titus in the foreground. Extraordinary composition, fewer tourists.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1580842943559-3a03c3b80de6?w=800&q=80" alt="Trevi Fountain Rome" onerror="this.src='https://images.unsplash.com/photo-1515542622106-78bda8ba0e5b?w=800&q=80'" />
          <span class="time-badge">15:30</span>
        </div>
        <div class="activity-tag">Roman Icons</div>
        <h3>Pantheon & Trevi Fountain</h3>
        <div class="activity-punchline">"The Pantheon's dome is still the world's greatest unreinforced concrete structure—built in 125 AD."</div>
        <div class="activity-desc">The Pantheon is one of the best-preserved ancient Roman buildings—its coffered concrete dome (43.3m diameter) inspired Brunelleschi's Florence dome and St. Peter's. The oculus at the top is the only source of light; on April 21 (Rome's birthday) the light beam lands exactly on the entrance. Then walk 10 minutes to the Trevi Fountain—throw one coin to return to Rome, two to fall in love, three to marry an Italian. Even in a crowd, it's magnificent.</div>
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(6)">← Prev</button>
      <span class="day-counter">Day 7 of 9</span>
      <button class="nav-btn" onclick="goTo(8)">Next →</button>
    </div>
  </div><!-- /page7 -->

  <!-- ============================================================
       DAY 8
  ============================================================ -->
  <div class="page" id="page8">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1531572753322-ad063cecc140?w=800&q=80" alt="Vatican St Peters Basilica" onerror="this.src='https://images.unsplash.com/photo-1552465011-b4e21bf6e79a?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 8 — Saturday</h2>
        <div class="sub">Vatican City</div>
        <div class="accommodation">🏨 Accommodation: Rome</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1531572753322-ad063cecc140?w=800&q=80" alt="St Peters Basilica" onerror="this.src='https://images.unsplash.com/photo-1513115045005-8a1a63a2ac08?w=800&q=80'" />
          <span class="time-badge">09:00</span>
        </div>
        <div class="activity-tag">Sacred Icon</div>
        <h3>St. Peter's Basilica & Dome</h3>
        <div class="activity-punchline">"The largest church on Earth—and the climb to the dome gives Rome to you in one sweep."</div>
        <div class="activity-desc">St. Peter's Basilica is the largest Christian church in the world (600ft long) and holds Michelangelo's <em>Pietà</em> behind glass in the first chapel on the right. Entry to the Basilica is free—but arrive by 9am before the queues form. The dome climb (551 steps or elevator partway) rewards with Rome's most panoramic views: Castel Sant'Angelo, the Tiber, the Forum, and on clear days, even the Castelli Romani hills.</div>
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1566438480900-0609be27a4be?w=800&q=80" alt="Sistine Chapel Vatican" onerror="this.src='https://images.unsplash.com/photo-1531572753322-ad063cecc140?w=800&q=80'" />
          <span class="time-badge">11:30</span>
        </div>
        <div class="activity-tag">Michelangelo</div>
        <h3>Sistine Chapel & Vatican Museums</h3>
        <div class="activity-punchline">"Michelangelo painted the ceiling lying on his back. Spend 4 years and see what he made."</div>
        <div class="activity-desc">The Vatican Museums are among the world's greatest art collections—25 museums, 54 galleries, 7km of corridors. The Gallery of Maps (40 gigantic topographical frescoes of Italy from 1580), the Raphael Rooms, and finally—the Sistine Chapel. Michelangelo's ceiling (painted 1508–1512) depicts 9 scenes from Genesis. Look for the famous <em>Creation of Adam</em>, but also the lesser-seen <em>Delphic Sibyl</em> and <em>Cumaean Sibyl</em>. The <em>Last Judgment</em> on the altar wall was added 25 years later. Book skip-the-line tickets (musei.vaticani.va) months in advance.</div>
      </div>

      <div class="tip-box">
        <strong>💡 Go early:</strong> First entry (8am) is the least crowded. Alternatively, book a night tour—the Sistine Chapel by torchlight is surreal.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1600623471616-8c1966c91ff6?w=800&q=80" alt="Trastevere Rome evening" onerror="this.src='https://images.unsplash.com/photo-1580842943559-3a03c3b80de6?w=800&q=80'" />
          <span class="time-badge">16:00</span>
        </div>
        <div class="activity-tag">Evening Rome</div>
        <h3>Piazza Navona & Trastevere</h3>
        <div class="activity-punchline">"Trastevere at night: fairy lights, cobblestones, laughter—this is the real Rome."</div>
        <div class="activity-desc">Piazza Navona was built on the footprint of Emperor Domitian's stadium (90 AD)—you can still see its oval shape. Bernini's <em>Fountain of the Four Rivers</em> (1651) dominates the square. Then cross the Tiber to Trastevere for dinner—a tangle of ivy-covered lanes that's one of Rome's most characterful neighbourhoods. Eat <em>cacio e pepe</em>, Rome's signature pasta: just pecorino, black pepper, and pasta water. Sounds simple. Isn't.</div>
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(7)">← Prev</button>
      <span class="day-counter">Day 8 of 9</span>
      <button class="nav-btn" onclick="goTo(9)">Next →</button>
    </div>
  </div><!-- /page8 -->

  <!-- ============================================================
       DAY 9
  ============================================================ -->
  <div class="page" id="page9">
    <div class="page-hero">
      <img src="https://images.unsplash.com/photo-1544928147-79a2dbc1f389?w=800&q=80" alt="Zurich city" onerror="this.src='https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?w=800&q=80'" />
      <div class="page-hero-overlay"></div>
      <div class="page-hero-text">
        <h2>Day 9 — Sunday</h2>
        <div class="sub">Rome → Zurich | Departure</div>
        <div class="accommodation">✈️ Flight home</div>
      </div>
    </div>

    <div class="page-body">

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1551866442-64e75e911c23?w=800&q=80" alt="Rome morning espresso" onerror="this.src='https://images.unsplash.com/photo-1513805959324-96eb66ca8713?w=800&q=80'" />
          <span class="time-badge">Morning</span>
        </div>
        <div class="activity-tag">Final Hours</div>
        <h3>Last Walk Through Rome</h3>
        <div class="activity-punchline">"Rome rewards the slow walker. The best thing about leaving is knowing you'll come back."</div>
        <div class="activity-desc">Wake early and revisit one favourite place before the city wakes up—the Trevi Fountain at 7am is a completely different experience than at noon. Grab a <em>cornetto</em> (croissant, always filled, always warm) with a standing espresso at a local bar—this is how Romans have breakfast, and it costs €1.50. Pick up souvenirs at Campo de' Fiori market (mornings only), or grab a bottle of olive oil and a tin of anchovies from a <em>salumeria</em>. Real Italian food gifts, not tourist trinkets.</div>
      </div>

      <div class="tip-box">
        <strong>🚌 Airport transfer:</strong> Leonardo Express train from Roma Termini to Fiumicino Airport (FCO) runs every 30 mins, takes 32 minutes. Allow 3h before departure. Do not take a taxi—the train is faster and cheaper.
      </div>

      <div class="divider"></div>

      <div class="activity">
        <div class="activity-img-wrap">
          <img src="https://images.unsplash.com/photo-1436491865332-7a61a109cc05?w=800&q=80" alt="Airport departure" onerror="this.src='https://images.unsplash.com/photo-1566408669374-5a6d5dca1ef5?w=800&q=80'" />
          <span class="time-badge">Departure</span>
        </div>
        <div class="activity-tag">Homeward</div>
        <h3>Flight Rome (FCO) → Zurich</h3>
        <div class="activity-punchline">"The Alps from above are the last postcard. Keep your eyes on the window."</div>
        <div class="activity-desc">The flight from Fiumicino to Zurich is just under 2 hours. On a clear day, the route passes over the Apennines, the Po Valley, and then the full arc of the Alps before descending into Switzerland. Keep a window seat if you can. Arrive in Zurich, collect luggage, and head home with 9 days of extraordinary memories—and, inevitably, a mental list of everything you'll do differently next time.</div>
      </div>

      <div class="tip-box">
        <strong>🎒 What to bring back:</strong> Chianti wine (Florence), Venetian glass (Venice), Limoncello (Rome), Swiss chocolate (Zurich airport, obviously). All fit in a carry-on if you pack smart.
      </div>

    </div>

    <div class="bottom-nav">
      <button class="nav-btn" onclick="goTo(8)">← Prev</button>
      <span class="day-counter">Day 9 of 9</span>
      <button class="nav-btn" disabled style="background:#b0c4b1;color:#fff">Bon Voyage ✈</button>
    </div>
  </div><!-- /page9 -->

</div><!-- /book -->

<script>
  const TOTAL = 9;
  let current = 1;

  function buildDots() {
    const container = document.getElementById('dots');
    container.innerHTML = '';
    for (let i = 1; i <= TOTAL; i++) {
      const d = document.createElement('div');
      d.className = 'dot' + (i === current ? ' active' : i < current ? ' visited' : '');
      d.onclick = () => goTo(i);
      d.style.cursor = 'pointer';
      container.appendChild(d);
    }
  }

  function goTo(n) {
    document.getElementById('page' + current).classList.remove('active');
    current = n;
    document.getElementById('page' + current).classList.add('active');
    // Scroll book back to top
    document.querySelector('.book').scrollTop = 0;
    window.scrollTo(0, 0);
    buildDots();
  }

  buildDots();
</script>

</body>
</html>
