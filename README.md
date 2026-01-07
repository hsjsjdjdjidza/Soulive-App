# Soulive-App
Aplikasi Live streaming buatan Indonesia 
import { useState, useEffect } from "react";

export default function SouliveApp() { const [screen, setScreen] = useState("splash"); const [username, setUsername] = useState(""); const [otp, setOtp] = useState(""); const [countdown, setCountdown] = useState(5);

useEffect(() => { if (screen === "splash") { const t = setTimeout(() => setScreen("auth"), 5000); return () => clearTimeout(t); } }, [screen]);

useEffect(() => { if (screen === "otp" && countdown > 0) { const t = setTimeout(() => setCountdown(countdown - 1), 1000); return () => clearTimeout(t); } if (screen === "otp" && countdown === 0) { setOtp("839201"); setTimeout(() => setScreen("terms"), 5000); } }, [screen, countdown]);

return ( <div className="min-h-screen flex flex-col items-center justify-center bg-white text-black"> {screen === "splash" && ( <div className="w-full h-screen flex flex-col items-center justify-end bg-cover" style={{ backgroundImage: "url(/foto1.jpg)" }}> <p className="mb-10 animate-pulse">Loading 5 detik...</p> </div> )}

{screen === "auth" && (
    <div className="space-y-4">
      <button onClick={() => setScreen("register")} className="px-6 py-2 bg-black text-white">Buat Akun Baru</button>
      <button className="px-6 py-2 border">Login ke Akun Lama</button>
    </div>
  )}

  {screen === "register" && (
    <div className="w-full max-w-md space-y-3">
      <button onClick={() => setScreen("auth")}>←</button>
      <h2 className="text-xl font-bold">Pendaftaran Akun</h2>
      <input placeholder="Nama Lengkap" className="border w-full p-2" />
      <input placeholder="Umur (Min 12)" className="border w-full p-2" />
      <input placeholder="Username" className="border w-full p-2" onChange={(e) => setUsername(e.target.value)} />
      <input placeholder="Asal Negara" className="border w-full p-2" />
      <input type="password" placeholder="Kata Sandi" className="border w-full p-2" />
      <button onClick={() => setScreen("otp")} className="w-full bg-black text-white py-2">Buat Akun Baru</button>
    </div>
  )}

  {screen === "otp" && (
    <div className="space-y-4">
      <h2 className="font-bold">Verifikasi</h2>
      <p>Kami akan memasukkan OTP otomatis</p>
      <div className="border w-64 h-10 flex items-center justify-center">{otp || "Menunggu OTP"}</div>
      <p>Hitung mundur: {countdown}</p>
    </div>
  )}

  {screen === "terms" && (
    <div className="max-w-lg space-y-3">
      <h2 className="font-bold">Syarat & Ketentuan</h2>
      <p>1. Live maksimal 12 jam/hari</p>
      <p>2. Spam komentar akan dikeluarkan</p>
      <p>3. Dilarang konten pornografi</p>
      <button onClick={() => setScreen("welcome")} className="bg-black text-white px-4 py-2">Ya, Saya Setuju</button>
    </div>
  )}

  {screen === "welcome" && (
    <div className="space-y-4">
      <h2>Selamat Datang {username}</h2>
      <p>Loading lagu...</p>
      {setTimeout(() => setScreen("home"), 2000)}
    </div>
  )}

  {screen === "home" && (
    <div className="w-full">
      <h1 className="text-center font-bold">Soulive App</h1>
      <nav className="fixed bottom-0 w-full flex justify-around border-t p-2 bg-white">
        <button>Live</button>
        <button>Cari</button>
        <button onClick={() => setScreen("plus")}>+</button>
        <button>Soul+</button>
        <button>Akun</button>
      </nav>
    </div>
  )}

  {screen === "plus" && (
    <div className="space-y-4">
      <h2>Mulai Live</h2>
      <button className="border p-3">Mulai live streaming dengan Soulive operator</button>
      <button className="border p-3">Live dari aplikasi lain</button>
    </div>
  )}
</div>

); }
