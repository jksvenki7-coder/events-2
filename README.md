# events-2import React, { useState } from 'react';

// Event Categories Component
const EventCategories = () => {
  const categories = [
    { title: 'Decoration', icon: '🎈' },
    { title: 'Catering', icon: '🍽️' },
    { title: 'Conventions', icon: '🏢' },
    { title: 'Photography & Videography', icon: '📸' },
    { title: 'Parlour & Accessories', icon: '💄' },
    { title: 'Anchors & Actors', icon: '🎤' },
    { title: 'DJ & Dance & Singers', icon: '🎶' },
    { title: 'Guest House & Rooms', icon: '🏠' },
    { title: 'Chocolates & Cakes', icon: '🍰' },
    { title: 'Games & Entertainment', icon: '🎯' },
    { title: 'Jewellery', icon: '💍' },
    { title: 'Invitation Cards', icon: '💌' },
    { title: 'Vehicles', icon: '🚗' },
    { title: 'Return Gifts', icon: '🎁' },
    { title: 'Decoration Items', icon: '🛒' },
    { title: 'Makeup Artist', icon: '💄' },
    { title: 'Mehandi Artist', icon: '🖌️' },
    { title: 'Clothing & Garments', icon: '👗' },
    { title: 'Purohith', icon: '🙏' },
  ];

  return (
    <div>
      <h2>Event Categories</h2>
      <div style={{ display: 'flex', flexWrap: 'wrap' }}>
        {categories.map((cat) => (
          <div key={cat.title} style={{
            border: '1px solid #ddd',
            borderRadius: '8px',
            width: '120px',
            height: '120px',
            margin: '8px',
            display: 'flex',
            flexDirection: 'column',
            alignItems: 'center',
            justifyContent: 'center',
            fontSize: '20px',
          }}>
            <div style={{ fontSize: '32px' }}>{cat.icon}</div>
            <div style={{ marginTop: '8px', textAlign: 'center' }}>{cat.title}</div>
          </div>
        ))}
      </div>
    </div>
  );
};

// Package Tiers Component
const PackageTiers = () => {
  const tierPrices = {
    Silver: '₹50,000 - ₹1,60,000',
    Gold: '₹1,90,000 - ₹3,00,000',
    Diamond: '₹3,00,000 - ₹5,00,000',
    Platinum: '₹5,00,000 - ₹8,00,000',
  };

  const [selectedTier, setSelectedTier] = useState('Silver');
  const [services, setServices] = useState({
    Decoration: 0,
    Catering: 0,
    'Parlour & Accessories': 0,
    'Anchors & Actors': 0,
    'DJ & Dance': 0,
    'Guest House & Room': 0,
    'Chocolates & Cakes': 0,
    'Games & Entertainment': 0,
    Jewellery: 0,
    'Invitation Cards': 0,
    Vehicles: 0,
    'Return Gifts': 0,
    'Makeup Artist': 0,
    'Mehandi Artist': 0,
    'Clothing & Garments': 0,
    Purohith: 0,
  });

  const increment = (service) => {
    setServices(prev => ({ ...prev, [service]: prev[service] + 1 }));
  };
  const decrement = (service) => {
    setServices(prev => ({ ...prev, [service]: Math.max(prev[service] - 1, 0) }));
  };

  return (
    <div>
      <h2>Package Tiers</h2>
      <div style={{ marginBottom: '16px' }}>
        {Object.keys(tierPrices).map(tier => (
          <button
            key={tier}
            onClick={() => setSelectedTier(tier)}
            style={{
              marginRight: '8px',
              backgroundColor: selectedTier === tier ? '#007BFF' : '#eee',
              color: selectedTier === tier ? '#fff' : '#000',
              border: 'none',
              padding: '8px 16px',
              borderRadius: '4px',
              cursor: 'pointer'
            }}
          >
            {tier}
          </button>
        ))}
      </div>
      <div>Price Range: {tierPrices[selectedTier]}</div>
      <div style={{ marginTop: '16px' }}>
        {Object.keys(services).map(service => (
          <div key={service} style={{ marginBottom: '10px' }}>
            <strong>{service}</strong> — 
            <button onClick={() => decrement(service)} style={{ marginLeft: '12px' }}>-</button>
            <span style={{ margin: '0 8px' }}>{services[service]}</span>
            <button onClick={() => increment(service)}>+</button>
          </div>
        ))}
      </div>
    </div>
  );
};

// Main App Component with Tabs
export default function App() {
  const [activeTab, setActiveTab] = useState('categories');

  return (
    <div style={{ padding: '20px', fontFamily: 'Arial, sans-serif' }}>
      <h1>Event & Catering Website</h1>
      <nav style={{ marginBottom: '20px' }}>
        <button onClick={() => setActiveTab('categories')} style={{ marginRight: '10px' }}>
          Event Categories
        </button>
        <button onClick={() => setActiveTab('packages')} style={{ marginRight: '10px' }}>
          Package Tiers
        </button>
      </nav>
      <div>
        {activeTab === 'categories' && <EventCategories />}
        {activeTab === 'packages' && <PackageTiers />}
      </div>
    </div>
  );
}
