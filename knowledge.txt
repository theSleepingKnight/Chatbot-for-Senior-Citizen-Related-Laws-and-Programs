// This is Lola Yan's Brain.
// We are adding a new feature:
// Use a "|" (pipe) character to split one answer into multiple chat bubbles.

const KNOWLEDGE_BASE = [
    // --- GREETINGS & BASIC ---
    {
        keywords: ['hello', 'hi', 'good morning', 'good afternoon', 'hey'],
        answer: "Hello there, apo!|I am Lola Yan, your NCSC Information Bot.|How can I assist you with Senior Citizen laws and benefits today?"
    },
    {
        keywords: ['thanks', 'thank you', 'salamat'],
        answer: "You're most welcome, apo!|It's my pleasure to help. Is there anything else you'd like to know?"
    },
    {
        keywords: ['bye', 'goodbye'],
        answer: "Goodbye, apo! Take care and don't hesitate to ask if you have more questions."
    },
    {
        keywords: ['who are you', 'your name', 'lola yan'],
        answer: "I am Lola Yan, the NCSC Information Bot.|I am here to help you understand the laws and services for senior citizens from the NCSC and DSWD."
    },

    // --- NCSC (National Commission of Senior Citizens) ---
    {
        keywords: ['ncsc', 'national commission'],
        answer: "The NCSC (National Commission of Senior Citizens) is the main government agency, created by RA 11350.|Its job is to ensure all laws and programs for the elderly are fully implemented."
    },
    {
        keywords: ['digital id', 'id card', 'ncsc id', 'paano mag-register'],
        answer: "The NCSC offers a free National Senior Citizen Digital ID.|You can register for it online through the NCSC website. This ID is a valid proof of identity to avail your benefits."
    },
    {
        keywords: ['ra 11350', 'ncsc law'],
        answer: "Republic Act No. 11350 is the law that created the National Commission of Senior Citizens (NCSC).|It gives the NCSC the power to ensure all other senior citizen laws are followed."
    },

    // --- DSWD (Department of Social Welfare and Development) ---
    {
        keywords: ['dswd', 'social welfare'],
        answer: "The DSWD is the lead agency for social services.|For seniors, they are primarily responsible for the Social Pension program."
    },
    {
        keywords: ['social pension', 'dswd pension', '1000 pension', 'indigent'],
        answer: "The Social Pension for Indigent Senior Citizens is managed by the DSWD.|It provides a monthly stipend of ₱1,000 to qualified seniors.|To qualify, you must be frail, sickly, have no regular income, and not be receiving pensions from SSS, GSIS, or other sources."
    },
    {
        keywords: ['aics', 'assistance', 'financial help', 'dswd help'],
        answer: "DSWD also provides financial or medical help through their AICS (Assistance to Individuals in Crisis Situation) program.|Senior citizens in crisis can apply for this at their nearest DSWD office."
    },

    // --- LAWS & BENEFITS (RA 9994, RA 11982) ---
    {
        keywords: ['discount', '20%'],
        answer: "Under RA 9994 (The Expanded Senior Citizens Act), you are entitled to a 20% discount AND VAT exemption.|This applies to things like medicine, food, public transport, and medical services."
    },
    {
        keywords: ['medicine', 'gamot', 'drugs', 'pharmacy'],
        answer: "Yes, apo, you get a 20% discount and VAT exemption on the purchase of all medicines (prescription or over-the-counter), vitamins, and mineral supplements.|Just present your Senior Citizen ID and purchase booklet."
    },
    {
        keywords: ['food', 'restaurant', 'jollibee', 'kain', 'grocery'],
        answer: "For restaurants, the 20% discount applies to food and drinks for your own consumption.|For groceries, there is a special 5% discount on certain basic necessities, with a limit of ₱1,300 per week."
    },
    {
        keywords: ['transportation', 'fare', 'jeep', 'bus', 'plane', 'boat', 'lrt', 'mrt'],
        answer: "Yes, you get a 20% discount on public transportation fares.|This includes jeepneys, buses, taxis, LRT/MRT, domestic flights, and sea travel."
    },
    {
        keywords: ['utilities', 'kuryente', 'tubig', 'electric', 'water bill'],
        answer: "You can get a 5% discount on your monthly water and electricity bills.|This is as long as the bill is under your name and your consumption is below a set limit (usually 100 kWh for electricity and 30 cubic meters for water)."
    },
    {
        keywords: ['medical', 'hospital', 'doctor', 'checkup', 'professional fee'],
        answer: "You get a 20% discount and VAT exemption on medical and dental services.|This includes doctor's professional fees, diagnostic tests (like X-rays, blood tests), and in-patient hospital room fees in private facilities."
    },
    {
        keywords: ['centenarian', '100 years old', 'ra 11982', '80', '85', '90', '95'],
        answer: "Great news, apo! Under the new Expanded Centenarians Act (RA 11982), Filipinos receive a ₱10,000 cash gift at ages 80, 85, 90, and 95.|Then, you will receive a ₱100,000 cash gift when you reach 100!"
    },
    {
        keywords: ['law', 'ra 9994', 'expanded senior citizens act'],
        answer: "The main law is Republic Act No. 9994, known as the 'Expanded Senior Citizens Act of 2010'.|It is the source of most benefits like the 20% discount and VAT exemption."
    },
    {
        keywords: ['philhealth', 'health insurance'],
        answer: "All senior citizens are automatically covered by PhilHealth (RA 10645).|This means you are entitled to health insurance benefits at any PhilHealth-accredited hospital or clinic."
    },
    {
        keywords: ['priority lane', 'express lane'],
        answer: "Yes, apo. All government and private establishments (like banks, supermarkets, and clinics) must have a priority or express lane for Senior Citizens, PWDs, and pregnant women."
    },
    {
        keywords: ['tax', 'income tax', 'exemption'],
        answer: "If you are a senior citizen and still working, your income is exempt from income tax, as long as you are earning the minimum wage or less."
    }
];

// This is the default answer if the bot doesn't find any keywords.
const DEFAULT_ANSWER = "I'm sorry, apo. I'm not sure I have the information for that...|Try asking in a different way, perhaps about 'discount', 'pension', or 'digital id'?";