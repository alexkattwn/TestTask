<script>
    import { pounds } from '../lib/format.js'

    import imgQS from '../../design/special-offers/assets/offer-QS-1209.png'
    import imgCH from '../../design/special-offers/assets/offer-CH-907.png'
    import imgYD from '../../design/special-offers/assets/offer-YD-708.png'
    import imgTR from '../../design/special-offers/assets/offer-TR-609.png'

    let { onbook = () => {} } = $props()

    const offers = [
        {
            id: 'QS-1209',
            building: 'Quayside',
            floor: 12,
            rooms: 2,
            area: 58.1,
            description: 'Water side, no balcony',
            price: 361800,
            oldPrice: 389000,
            image: imgQS,
            alt: 'Living room with large windows overlooking the water',
        },
        {
            id: 'CH-907',
            building: 'Crane House',
            floor: 9,
            rooms: 2,
            area: 58.4,
            description: 'North-west corner, balcony over the courtyard',
            price: 311100,
            oldPrice: 334500,
            image: imgCH,
            alt: 'Living room with red crane view',
        },
        {
            id: 'YD-708',
            building: 'Yard',
            floor: 7,
            rooms: 2,
            area: 70.3,
            description: 'South-east corner, balcony over the courtyard',
            price: 339900,
            oldPrice: 365500,
            image: imgYD,
            alt: 'Dining area with large windows',
        },
        {
            id: 'TR-609',
            building: 'Terrace',
            floor: 6,
            rooms: 2,
            area: 74.8,
            description: 'Old town side, balcony facing the old town',
            price: 382200,
            oldPrice: 411000,
            image: imgTR,
            alt: 'Living room with sofa and balcony view',
        },
    ]

    function bookViewing() {
        onbook()
    }
</script>

<section class="special">
    <div class="special-inner">
        <header class="special-head">
            <h2 class="special-title">Special offers</h2>
            <p class="special-note">
                Four homes at 7% off the list price<br />
                until 31 December.
            </p>
        </header>

        <div class="special-track">
            {#each offers as offer}
                <article class="offer-card">
                    <div class="offer-photo">
                        <img src={offer.image} alt={offer.alt} loading="lazy" width="326" height="408" />
                    </div>

                    <div class="offer-body">
                        <p class="offer-building">{offer.building}, floor {offer.floor}</p>
                        <p class="offer-meta">{offer.rooms} bedrooms, {offer.area} m²</p>
                        <p class="offer-desc">{offer.description}</p>

                        <div class="offer-price">
                            <span class="price-new">{pounds(offer.price)}</span>
                            <span class="price-old">{pounds(offer.oldPrice)}</span>
                        </div>

                        <button class="offer-link" type="button" onclick={bookViewing}>
                            Book a viewing
                        </button>
                    </div>
                </article>
            {/each}
        </div>
    </div>
</section>

<style>
    /* Десктоп / 1440 */
    .special {
        --special-pad-y: 120px;
        padding: var(--special-pad-y) 0;
        background: #eeecea;
    }

    .special-inner {
        max-width: 1440px;
        margin: 0 auto;
        padding: 0 32px;
    }

    .special-head {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 32px;
        margin-bottom: 40px;
    }

    .special-title {
        margin: 0;
        font-family: 'Newsreader', serif;
        font-size: 56px;
        font-weight: 300;
        line-height: 1.05;
        letter-spacing: -0.03em;
        color: #333231;
    }

    .special-note {
        max-width: 24ch;
        margin: 0;
        font-size: 16px;
        line-height: 1.35;
        color: #6b6763;
        text-align: right;
    }

    .special-track {
        display: grid;
        grid-template-columns: repeat(4, minmax(0, 1fr));
        gap: 20px;
    }

    .offer-card {
        display: flex;
        flex-direction: column;
        min-width: 0;
    }

    .offer-photo {
        position: relative;
        aspect-ratio: 4 / 5;
        overflow: hidden;
        background: #e4e1dc;
    }

    .offer-photo img {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: transform 0.7s cubic-bezier(0.22, 1, 0.36, 1);
    }

    .offer-card:hover .offer-photo img {
        transform: scale(1.04);
    }

    .offer-body {
        padding-top: 12px;
    }

    .offer-building {
        margin: 0 0 2px;
        font-size: 12px;
        line-height: 1.3;
        color: #6b6763;
    }

    .offer-meta {
        margin: 0;
        font-size: 18px;
        font-weight: 400;
        line-height: 1.25;
        color: #333231;
    }

    .offer-desc {
        margin: 3px 0 0;
        font-size: 12px;
        line-height: 1.35;
        color: #6b6763;
    }

    .offer-price {
        display: flex;
        align-items: baseline;
        gap: 8px;
        margin-top: 10px;
    }

    .price-new {
        font-size: 18px;
        font-weight: 500;
        letter-spacing: -0.01em;
        font-variant-numeric: tabular-nums;
        color: #333231;
    }

    .price-old {
        font-size: 12px;
        color: #8a8580;
        text-decoration: line-through;
        font-variant-numeric: tabular-nums;
    }

    .offer-link {
        display: inline-block;
        margin-top: 10px;
        padding: 0;
        border: 0;
        background: none;
        font: inherit;
        font-size: 13px;
        color: #333231;
        text-decoration: underline;
        text-underline-offset: 0.22em;
        text-decoration-thickness: 0.07em;
        cursor: pointer;
    }

    .offer-link:hover {
        color: var(--accent, #c45c26);
    }

    /* Планшеты / 768 */
     @media (max-width: 1024px) {
        .special {
            --special-pad-y: 80px;
        }

        .special-inner {
            padding: 0 24px;
        }

        .special-head {
            align-items: flex-start;
            gap: 24px;
            margin-bottom: 32px;
        }

        .special-title {
            font-size: 44px;
        }

        .special-note {
            font-size: 14px;
            text-align: right;
        }

        .special-track {
            display: grid !important;
            grid-template-columns: repeat(2, minmax(0, 1fr)) !important;
            gap: 28px 20px;
            overflow-x: visible;
        }

        .offer-card {
            flex: none;
            width: auto;
        }
    }

    /* Смартфоны / 375 */
    @media (max-width: 640px) {
        .special {
            --special-pad-y: 64px;
        }

        .special-inner {
            padding: 0 16px;
        }

        .special-head {
            flex-direction: column;
            align-items: flex-end;
            gap: 10px;
            margin-bottom: 24px;
        }

        .special-title {
            align-self: flex-start;
            font-size: 32px;
        }

        .special-note {
            max-width: 22ch;
            font-size: 12px;
            text-align: right;
        }

        .special-track {
            display: flex;
            gap: 12px;
            overflow-x: auto;
            scroll-snap-type: x mandatory;
            scroll-padding-left: 16px;
            margin: 0 -16px;
            padding: 0 16px 6px;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none;
        }

        .special-track::-webkit-scrollbar {
            display: none;
        }

        .offer-card {
            flex: 0 0 264px;
            scroll-snap-align: start;
        }

        .offer-meta,
        .price-new {
            font-size: 16px;
        }
    }
</style>