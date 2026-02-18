# Nhi2
import React, { useState } from "react";

export default function PrivateStoryWebsite() { const [name, setName] = useState(""); const [story, setStory] = useState(""); const [submitted, setSubmitted] = useState(false);

const handleSubmit = async (e) => { e.preventDefault();

// Gửi dữ liệu đến API backend của bạn
await fetch("/api/submit-story", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ name, story }),
});

setSubmitted(true);
setName("");
setStory("");

};

return ( <div className="min-h-screen bg-gray-100 flex items-center justify-center p-6"> <div className="bg-white shadow-xl rounded-2xl p-8 w-full max-w-xl"> <h1 className="text-2xl font-bold mb-4 text-center"> Chia sẻ câu chuyện của bạn (Riêng tư) </h1>

{submitted ? (
      <p className="text-green-600 text-center">
        Cảm ơn bạn! Câu chuyện đã được gửi riêng đến quản trị viên.
      </p>
    ) : (
      <form onSubmit={handleSubmit} className="space-y-4">
        <div>
          <label className="block mb-1 font-medium">Tên của bạn</label>
          <input
            type="text"
            value={name}
            onChange={(e) => setName(e.target.value)}
            className="w-full border rounded-lg p-2"
            placeholder="Ẩn danh nếu muốn"
          />
        </div>

        <div>
          <label className="block mb-1 font-medium">Câu chuyện của bạn</label>
          <textarea
            value={story}
            onChange={(e) => setStory(e.target.value)}
            className="w-full border rounded-lg p-2 h-40"
            required
            placeholder="Viết câu chuyện của bạn ở đây..."
          />
        </div>

        <button
          type="submit"
          className="w-full bg-black text-white py-2 rounded-xl hover:opacity-90"
        >
          Gửi câu chuyện
        </button>
      </form>
    )}
  </div>
</div>

); }

/*

BACKEND (Node.js - Express) Tạo file: /api/submit-story.js (hoặc server.js nếu dùng Express riêng)

import fs from "fs"
