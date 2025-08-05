# Winkelkassa
import React, { useState } from "react";

const producten = {
  "Groente & Fruit": [
    { naam: "Appels", prijs: 1.00 },
    { naam: "Peren", prijs: 1.10 },
    { naam: "Bananen", prijs: 0.80 },
    { naam: "Sinaasappels", prijs: 1.20 },
    { naam: "Mango's", prijs: 1.50 },
    { naam: "Ananas", prijs: 2.00 },
    { naam: "Kiwi’s", prijs: 1.30 },
    { naam: "Druiven", prijs: 2.20 },
    { naam: "Aardbeien", prijs: 2.50 },
    { naam: "Blauwe bessen", prijs: 2.50 },
    { naam: "Frambozen", prijs: 2.50 },
    { naam: "Tomaten", prijs: 1.10 },
    { naam: "Komkommers", prijs: 0.90 },
    { naam: "Paprika’s", prijs: 1.30 },
    { naam: "Wortels", prijs: 0.70 },
    { naam: "Broccoli", prijs: 1.20 },
    { naam: "Bloemkool", prijs: 1.50 },
    { naam: "Spinazie", prijs: 1.80 },
    { naam: "Boerenkool", prijs: 1.70 },
    { naam: "Sla", prijs: 1.00 },
    { naam: "Avocado", prijs: 1.60 },
    { naam: "Uien", prijs: 0.60 },
    { naam: "Knoflook", prijs: 0.50 },
    { naam: "Prei", prijs: 0.90 },
    { naam: "Courgette", prijs: 1.10 },
    { naam: "Aubergine", prijs: 1.20 },
    { naam: "Champignons", prijs: 1.50 },
    { naam: "Radijs", prijs: 0.80 },
    { naam: "Bleekselderij", prijs: 1.00 },
  ],
  "Vlees, Vis & Vleesvervangers": [
    { naam: "Kipfilet", prijs: 5.00 },
    { naam: "Gehakt", prijs: 4.50 },
    { naam: "Biefstuk", prijs: 8.00 },
    { naam: "Speklapjes", prijs: 5.50 },
    { naam: "Varkenshaas", prijs: 7.00 },
    { naam: "Worstjes", prijs: 4.00 },
    { naam: "Schnitzel", prijs: 6.00 },
    { naam: "Zalm", prijs: 10.00 },
    { naam: "Tonijn", prijs: 9.00 },
    { naam: "Kabeljauw", prijs: 8.50 },
    { naam: "Garnalen", prijs: 12.00 },
    { naam: "Haring", prijs: 6.50 },
    { naam: "Makreel", prijs: 7.00 },
    { naam: "Tofu", prijs: 3.50 },
    { naam: "Tempeh", prijs: 3.50 },
    { naam: "Vegetarische burgers", prijs: 4.00 },
    { naam: "Falafel", prijs: 3.00 },
    { naam: "Plantaardige balletjes", prijs: 3.00 },
  ],
  "Zuivel & Eieren": [
    { naam: "Melk vol", prijs: 1.20 },
    { naam: "Melk halfvol", prijs: 1.10 },
    { naam: "Melk mager", prijs: 1.00 },
    { naam: "Yoghurt", prijs: 1.30 },
    { naam: "Kwark", prijs: 1.50 },
    { naam: "Karnemelk", prijs: 1.10 },
    { naam: "Slagroom", prijs: 1.50 },
    { naam: "Kaas jong", prijs: 3.50 },
    { naam: "Kaas belegen", prijs: 3.70 },
    { naam: "Kaas oud", prijs: 4.00 },
    { naam: "Geitenkaas", prijs: 4.20 },
    { naam: "Mozzarella", prijs: 3.50 },
    { naam: "Feta", prijs: 3.80 },
    { naam: "Parmezaan", prijs: 5.00 },
    { naam: "Boter", prijs: 2.00 },
    { naam: "Margarine", prijs: 1.80 },
    { naam: "Eieren scharrel", prijs: 2.50 },
    { naam: "Eieren biologisch", prijs: 3.00 },
  ],
  "Brood & Banket": [
    { naam: "Witbrood", prijs: 2.00 },
    { naam: "Bruinbrood", prijs: 2.00 },
    { naam: "Volkorenbrood", prijs: 2.20 },
    { naam: "Zuurdesem", prijs: 2.50 },
    { naam: "Croissants", prijs: 1.50 },
    { naam: "Stokbrood", prijs: 1.80 },
    { naam: "Pistolets", prijs: 1.20 },
    { naam: "Bagels", prijs: 1.80 },
    { naam: "Beschuit", prijs: 1.00 },
    { naam: "Crackers", prijs: 1.20 },
    { naam: "Knäckebröd", prijs: 1.10 },
    { naam: "Rijstwafels", prijs: 1.00 },
    { naam: "Koekjes", prijs: 1.50 },
    { naam: "Cakes", prijs: 2.00 },
    { naam: "Muffins", prijs: 1.80 },
    { naam: "Donuts", prijs: 1.20 },
    { naam: "Taarten", prijs: 10.00 },
  ],
  // Hier kun je de rest toevoegen volgens je lijst
};

export default function KassaSimulator() {
  const [gekozenCategorie, setGekozenCategorie] = useState(null);
  const [winkelwagen, setWinkelwagen] = useState({});
  const [korting, setKorting] = useState(0);
  const [kortingInvoeren, setKortingInvoeren] = useState(false);
  const [betaalKeuze, setBetaalKeuze] = useState(null);

  function voegToe(product) {
    setWinkelwagen((prev) => {
      const nieuweAantal = (prev[product.naam]?.aantal || 0) + 1;
      return {
        ...prev,
        [product.naam]: { ...product, aantal: nieuweAantal },
      };
    });
  }

  function verwijder(productNaam) {
    setWinkelwagen((prev) => {
      const nieuw = { ...prev };
      if (nieuw[productNaam]) {
        if (nieuw[productNaam].aantal > 1) {
          nieuw[productNaam].aantal -= 1;
        } else {
          delete nieuw[productNaam];
        }
      }
      return nieuw;
    });
  }

  function totaalPrijs() {
    const totaal = Object.values(winkelwagen).reduce(
      (acc, p) => acc + p.prijs * p.aantal,
      0
    );
    return totaal * ((100 - korting) / 100);
  }

  return (
    <div style={{ padding: 20, fontFamily: "Arial, sans-serif", maxWidth: 600, margin: "auto" }}>
      {!gekozenCategorie ? (
        <>
          <h1>Kies een categorie</h1>
          <ul style={{ listStyle: "none", paddingLeft: 0 }}>
            {Object.keys(producten).map((cat) => (
              <li
                key={cat}
                style={{
                  cursor: "pointer",
                  padding: 10,
                  border: "1px solid #ccc",
                  marginBottom: 6,
                  borderRadius: 6,
                }}
                onClick={() => setGekozenCategorie(cat)}
              >
                {cat}
              </li>
            ))}
          </ul>
        </>
      ) : (
        <>
          <button onClick={() => setGekozenCategorie(null)} style={{ marginBottom: 20 }}>
            ← Terug naar categorieën
          </button>
          <h2>{gekozenCategorie}</h2>
          <ul style={{ listStyle: "none", paddingLeft: 0 }}>
            {producten[gekozenCategorie].map((product) => (
              <li
                key={product.naam}
                style={{
                  borderBottom: "1px solid #eee",
                  padding: 8,
                  display: "flex",
                  justifyContent: "space-between",
                  alignItems: "center",
                }}
              >
                <span>
                  {product.naam} — €{product.prijs.toFixed(2)}
                </span>
                <button onClick={() => voegToe(product)}>+ Toevoegen</button>
              </li>
            ))}
          </ul>
        </>
      )}

      <hr />

      <h2>Winkelwagen</h2>
      {Object.keys(winkelwagen).length === 0 ? (
        <p>Je winkelwagen is leeg</p>
      ) : (
        <>
          {Object.values(winkelwagen).map((item) => (
            <div
              key={item.naam}
              style={{
                marginBottom: 12,
                display: "flex",
                justifyContent: "space-between",
                alignItems: "center",
              }}
            >
              <span>
                {item.naam} — {item.aantal} × €{item.prijs.toFixed(2)} = €
                {(item.aantal * item.prijs).toFixed(2)}
              </span>
              <span>
                <button onClick={() => voegToe(item)}>+</button>{" "}
                <button onClick={() => verwijder(item.naam)}>-</button>
              </span>
            </div>
          ))}

          {!kortingInvoeren ? (
            <button onClick={() => setKortingInvoeren(true)} style={{ marginBottom: 10 }}>
              Korting invoeren
            </button>
          ) : (
            <div style={{ marginBottom: 10 }}>
              <input
                type="number"
                value={korting}
                onChange={(e) => setKorting(Number(e.target.value))}
                min={0}
                max={100}
                placeholder="Kortingspercentage"
                style={{ width: 120, marginRight: 10 }}
              />
              <button onClick={() => setKortingInvoeren(false)}>Bevestigen</button>
            </div>
          )}

          <h3>Totaal: €{totaalPrijs().toFixed(2)}</h3>

          {!betaalKeuze ? (
            <>
              <p>Betaal met:</p>
              <button onClick={() => setBetaalKeuze("bancontact")} style={{ marginRight: 10 }}>
                Bancontact
              </button>
              <button onClick={() => setBetaalKeuze("cash")}>Cash</button>
            </>
          ) : (
            <>
              {betaalKeuze === "bancontact" && (
                <>
                  <p>Scan de QR-code hieronder om te betalen (demo QR-code):</p>
                  <img
                    src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=bancontact-demo"
                    alt="Bancontact QR-code"
                  />
                </>
              )}
              {betaalKeuze === "cash" && <p>Betaal contant aan de kassa.</p>}

              <button
                onClick={() => {
                  setWinkelwagen({});
                  setKorting(0);
                  setBetaalKeuze(null);
                }}
                style={{ marginTop: 10 }}
              >
                Transactie afronden
              </button>
            </>
          )}
        </>
      )}
    </div>
  );
}
