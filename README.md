import React, { useState, useEffect } from "react";

const ValentineApp = () => {
    const [countdown, setCountdown] = useState("");
    
    useEffect(() => {
        const targetDate = new Date("February 14, 2025 00:00:00").getTime();
        const interval = setInterval(() => {
            const now = new Date().getTime();
            const difference = targetDate - now;

            if (difference < 0) {
                clearInterval(interval);
                setCountdown("Happy Valentine's Day! ❤️");
                return;
            }
            
            const days = Math.floor(difference / (1000 * 60 * 60 * 24));
            const hours = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((difference % (1000 * 60)) / 1000);
            
            setCountdown(`${days}d ${hours}h ${minutes}m ${seconds}s`);
        }, 1000);
        
        return () => clearInterval(interval);
    }, []);

    const [noPosition, setNoPosition] = useState({ top: "50%", left: "50%" });
    
    const moveButton = () => {
        const x = Math.random() * (window.innerWidth - 100);
        const y = Math.random() * (window.innerHeight - 50);
        setNoPosition({ top: `${y}px`, left: `${x}px` });
    };

    const sayYes = () => {
        alert("Yay! I love you! ❤️");
    };

    return (
        <div className="flex flex-col items-center justify-center h-screen bg-pink-200 text-center">
            <h1 className="text-3xl font-bold">Will you be my Valentine? ❤️</h1>
            <p className="text-lg mt-4">Countdown to Valentine: {countdown}</p>
            <div className="mt-6 flex gap-4">
                <button className="bg-red-500 text-white px-6 py-3 rounded-lg text-xl" onClick={sayYes}>
                    Yes
                </button>
                <button 
                    className="bg-gray-500 text-white px-6 py-3 rounded-lg text-xl absolute"
                    style={{ top: noPosition.top, left: noPosition.left }}
                    onMouseOver={moveButton}
                >
                    No
                </button>
            </div>
            <audio autoPlay loop>
                <source src="love-song.mp3" type="audio/mpeg" />
            </audio>
        </div>
    );
};

export default ValentineApp;
