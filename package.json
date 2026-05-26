const express = require('express');
const { GoogleGenerativeAI } = require("@google/generative-ai");

const app = express();
app.use(express.json());

// استخدام process.env.API_KEY بدلاً من وضع المفتاح مباشرة
const genAI = new GoogleGenerativeAI(process.env.API_KEY);

app.post('/ask', async (req, res) => {
    const question = req.body.question;
    if (!question) return res.status(400).json({ error: "لا يوجد سؤال!" });

    try {
        const model = genAI.getGenerativeModel({ model: "gemini-1.5-flash" });
        const result = await model.generateContent(question);
        const response = await result.response;
        res.json({ answer: response.text() });
    } catch (error) {
        console.error(error);
        res.status(500).json({ error: "خطأ في الاتصال بالـ AI" });
    }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server is running on port ${PORT}`));
