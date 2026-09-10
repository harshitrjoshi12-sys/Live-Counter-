import React, { useState, useRef } from 'react';
import { Camera, Plus, Minus, Trash2, CheckCircle, Share2 } from 'lucide-react';

export default function App() {
  const [truckNo, setTruckNo] = useState('');
  const [count, setCount] = useState(54);
  const [dhaangList, setDhaangList] = useState([]);
  const [capturedImage, setCapturedImage] = useState(null);
  const fileInputRef = useRef(null);

  const handleCapture = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => setCapturedImage(reader.result);
      reader.readAsDataURL(file);
    }
  };

  const handleSaveDhaang = () => {
    if (count <= 0) return;
    const newDhaang = {
      id: Date.now(),
      count: Number(count),
      image: capturedImage,
      time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    };
    setDhaangList([...dhaangList, newDhaang]);
    setCapturedImage(null);
    setCount(54);
  };

  const handleDeleteDhaang = (id) => {
    setDhaangList(dhaangList.filter(d => d.id !== id));
  };

  const totalBags = dhaangList.reduce((sum, item) => sum + item.count, 0);

  const handleShareWhatsApp = () => {
    let msg = `*TRUCK LOADING SUMMARY*\n`;
    msg += `Truck No: ${truckNo || 'N/A'}\n`;
    msg += `Date: ${new Date().toLocaleDateString()}\n`;
    msg += `------------------------\n`;
    dhaangList.forEach((d, i) => {
      msg += `Dhaang ${i + 1}: ${d.count} Bags (${d.time})\n`;
    });
    msg += `------------------------\n`;
    msg += `*TOTAL: ${totalBags} Bags*\n`;
    window.open(`https://wa.me/?text=${encodeURIComponent(msg)}`, '_blank');
  };

  return (
    <div className="min-h-screen bg-slate-900 text-slate-100 p-4 max-w-md mx-auto font-sans pb-16">
      <div className="border-b border-slate-800 pb-3 mb-4">
        <h1 className="text-xl font-black text-amber-400">COUNT APPLICATION</h1>
        <p className="text-xs text-slate-400">Truck Dhaang & Bag Counter</p>
      </div>

      <div className="bg-slate-800 p-3 rounded-xl mb-4 border border-slate-700">
        <label className="text-xs text-slate-400 block mb-1">Truck Number</label>
        <input 
          type="text" 
          placeholder="RJ-21-GB-XXXX"
          value={truckNo}
          onChange={(e) => setTruckNo(e.target.value.toUpperCase())}
          className="w-full bg-slate-900 border border-slate-700 rounded-lg px-3 py-2 text-white uppercase font-semibold focus:outline-none focus:border-amber-400"
        />
      </div>

      <div className="bg-slate-800 p-4 rounded-xl mb-4 border border-slate-700 text-center">
        <input 
          type="file" 
          accept="image/*" 
          capture="environment" 
          ref={fileInputRef} 
          onChange={handleCapture} 
          className="hidden" 
        />

        {capturedImage ? (
          <div className="relative mb-3">
            <img src={capturedImage} alt="Dhaang Preview" className="w-full h-44 object-cover rounded-lg border border-amber-400/50" />
            <button 
              onClick={() => setCapturedImage(null)}
              className="absolute top-2 right-2 bg-red-600 text-white text-xs px-2 py-1 rounded shadow"
            >
              Retake
            </button>
          </div>
        ) : (
          <button 
            onClick={() => fileInputRef.current?.click()}
            className="w-full py-6 border-2 border-dashed border-slate-600 rounded-xl flex flex-col items-center justify-center hover:border-amber-400 transition"
          >
            <Camera className="w-9 h-9 text-amber-400 mb-1" />
            <span className="text-sm font-semibold">Dhaang Ki Photo Lo</span>
            <span className="text-xs text-slate-400">Phone Camera se photo capture hogi</span>
          </button>
        )}

        <div className="mt-3">
          <label className="text-xs text-slate-400 block mb-2">Bags Confirm Karo</label>
          <div className="flex items-center justify-center gap-4">
            <button 
              onClick={() => setCount(prev => Math.max(1, prev - 1))}
              className="w-11 h-11 rounded-full bg-slate-700 active:bg-slate-600 flex items-center justify-center text-xl font-bold"
            >
              <Minus className="w-5 h-5" />
            </button>

            <span className="text-4xl font-black text-amber-400 w-20 text-center">{count}</span>

            <button 
              onClick={() => setCount(prev => prev + 1)}
              className="w-11 h-11 rounded-full bg-slate-700 active:bg-slate-600 flex items-center justify-center text-xl font-bold"
            >
              <Plus className="w-5 h-5" />
            </button>
          </div>

          <div className="flex justify-center gap-2 mt-3">
            {[50, 54, 55, 60].map(val => (
              <button 
                key={val} 
                onClick={() => setCount(val)}
                className={`text-xs px-3 py-1.5 rounded-lg border ${count === val ? 'bg-amber-400 text-black border-amber-400 font-bold' : 'bg-slate-700 border-slate-600 text-slate-300'}`}
              >
                {val} Dhaang
              </button>
            ))}
          </div>

          <button 
            onClick={handleSaveDhaang}
            className="w-full mt-4 bg-amber-400 text-black font-bold py-3 rounded-lg flex items-center justify-center gap-2 active:bg-amber-500 shadow-md"
          >
            <CheckCircle className="w-5 h-5" /> Dhaang Save Karo
          </button>
        </div>
      </div>

      <div className="bg-slate-800 p-4 rounded-xl border border-slate-700 mb-4">
        <div className="flex justify-between items-center mb-3">
          <h2 className="font-bold text-sm">Loaded Dhaange ({dhaangList.length})</h2>
          <div className="text-right">
            <span className="text-xs text-slate-400">Total: </span>
            <span className="text-lg font-black text-amber-400">{totalBags} Bags</span>
          </div>
        </div>

        {dhaangList.length === 0 ? (
          <p className="text-center text-xs text-slate-500 py-3">Abhi tak koi dhaang add nahi hui</p>
        ) : (
          <div className="space-y-2 max-h-52 overflow-y-auto">
            {dhaangList.map((d, index) => (
              <div key={d.id} className="flex items-center justify-between bg-slate-900 p-2.5 rounded-lg border border-slate-800">
                <div className="flex items-center gap-3">
                  {d.image && <img src={d.image} alt="thumb" className="w-10 h-10 object-cover rounded" />}
                  <div>
                    <span className="text-sm font-bold">Dhaang #{index + 1}</span>
                    <span className="text-xs text-slate-400 block">{d.time}</span>
                  </div>
                </div>
                <div className="flex items-center gap-3">
                  <span className="text-base font-black text-amber-400">{d.count} Bags</span>
                  <button onClick={() => handleDeleteDhaang(d.id)} className="text-slate-500 hover:text-red-400 p-1">
                    <Trash2 className="w-4 h-4" />
                  </button>
                </div>
              </div>
            ))}
          </div>
        )}
      </div>

      {dhaangList.length > 0 && (
        <button 
          onClick={handleShareWhatsApp}
          className="w-full bg-emerald-600 text-white font-bold py-3 rounded-lg flex items-center justify-center gap-2 active:bg-emerald-700 shadow-md"
        >
          <Share2 className="w-5 h-5" /> WhatsApp Par Bhejo
        </button>
      )}
    </div>
  );
}
