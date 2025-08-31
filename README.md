# Helalink-org
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HelaLink Agencies</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://unpkg.com/react-router-dom@6/dist/umd/react-router-dom.development.js"></script>
    <script src="https://unpkg.com/framer-motion@10/dist/framer-motion.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/lucide-react@0.263.1/dist/umd/lucide-react.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        slate: {
                            100: '#f1f5f9',
                            200: '#e2e8f0',
                            300: '#cbd5e1',
                            400: '#94a3b8',
                            500: '#64748b',
                            600: '#475569',
                            700: '#334155',
                            800: '#1e293b',
                            900: '#0f172a',
                            950: '#020617'
                        },
                        emerald: {
                            300: '#6ee7b7',
                            400: '#34d399',
                            500: '#10b981'
                        },
                        cyan: {
                            400: '#22d3ee'
                        },
                        rose: {
                            300: '#fda4af'
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif;
        }
        .bg-gradient-custom {
            background: linear-gradient(135deg, #020617 0%, #1e293b 50%, #0f172a 100%);
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useMemo, useState, useEffect } = React;
        const { BrowserRouter, Routes, Route, Link, useNavigate } = ReactRouterDOM;
        const { motion } = FramerMotion;
        
        // Custom UI components since we can't import from "@/components/ui"
        function Button({ children, className = "", variant = "default", size = "default", ...props }) {
            const baseClasses = "inline-flex items-center justify-center rounded-md text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-slate-400 focus-visible:ring-offset-2 disabled:opacity-50 disabled:pointer-events-none";
            const variants = {
                default: "bg-emerald-500 text-white hover:bg-emerald-600",
                secondary: "bg-slate-800 text-slate-100 hover:bg-slate-700",
                ghost: "bg-transparent hover:bg-slate-800 text-slate-100"
            };
            const sizes = {
                default: "h-10 py-2 px-4",
                lg: "h-11 px-8 rounded-md"
            };
            
            return React.createElement('button', {
                className: `${baseClasses} ${variants[variant]} ${sizes[size]} ${className}`,
                ...props
            }, children);
        }
        
        function Card({ children, className = "" }) {
            return React.createElement('div', {
                className: `rounded-lg border border-slate-700 bg-slate-800 text-slate-100 shadow-sm ${className}`
            }, children);
        }
        
        function CardHeader({ children, className = "" }) {
            return React.createElement('div', {
                className: `flex flex-col space-y-1.5 p-6 ${className}`
            }, children);
        }
        
        function CardTitle({ children, className = "" }) {
            return React.createElement('h3', {
                className: `text-lg font-semibold leading-none tracking-tight ${className}`
            }, children);
        }
        
        function CardContent({ children, className = "" }) {
            return React.createElement('div', {
                className: `p-6 pt-0 ${className}`
            }, children);
        }
        
        function Input({ className = "", ...props }) {
            return React.createElement('input', {
                className: `flex h-10 w-full rounded-md border border-slate-700 bg-slate-800 px-3 py-2 text-sm ring-offset-slate-900 file:border-0 file:bg-transparent file:text-sm file:font-medium placeholder:text-slate-500 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-slate-400 focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50 ${className}`,
                ...props
            });
        }
        
        function Textarea({ className = "", ...props }) {
            return React.createElement('textarea', {
                className: `flex min-h-[80px] w-full rounded-md border border-slate-700 bg-slate-800 px-3 py-2 text-sm ring-offset-slate-900 placeholder:text-slate-500 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-slate-400 focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50 ${className}`,
                ...props
            });
        }
        
        function Badge({ children, className = "" }) {
            return React.createElement('span', {
                className: `inline-flex items-center rounded-full border border-slate-700 px-2.5 py-0.5 text-xs font-semibold transition-colors focus:outline-none focus:ring-2 focus:ring-slate-400 focus:ring-offset-2 ${className}`
            }, children);
        }

        // ====== CONFIG (edit freely) ====== 
        const BRAND = { 
            name: "HelaLink Agencies", 
            whatsapp: "https://wa.me/254777739948", 
            register: "https://helalink.com/register.php?ref=TeejaeyKe", 
            email: "mailto:teejaeyke@gmail.com", 
        };

        // ====== LAYOUT ====== 
        function Shell({ children }) { 
            return React.createElement('div', { className: "min-h-screen bg-gradient-custom text-slate-100" },
                React.createElement(TopNav),
                React.createElement('main', { className: "mx-auto max-w-6xl px-4 pb-24 pt-24 md:pt-28" }, children),
                React.createElement(Footer),
                React.createElement(WhatsAppFAB)
            ); 
        }

        function TopNav() { 
            const [open, setOpen] = useState(false); 
            return React.createElement('header', { className: "fixed inset-x-0 top-0 z-50 bg-slate-900/60 backdrop-blur border-b border-white/10" },
                React.createElement('nav', { className: "mx-auto flex max-w-6xl items-center justify-between px-4 py-3" },
                    React.createElement(Link, { to: "/", className: "flex items-center gap-2" },
                        React.createElement('div', { className: "h-9 w-9 rounded-2xl bg-gradient-to-br from-emerald-400 to-cyan-400" }),
                        React.createElement('span', { className: "font-semibold tracking-wide" }, BRAND.name)
                    ),
                    React.createElement('div', { className: "hidden items-center gap-1 md:flex" },
                        React.createElement(NavLink, { to: "/", label: "Home", icon: React.createElement(LucideReact.HomeIcon, { className: "h-4 w-4" }) }),
                        React.createElement(NavLink, { to: "/earn", label: "Ways to Earn", icon: React.createElement(LucideReact.HandCoins, { className: "h-4 w-4" }) }),
                        React.createElement(NavLink, { to: "/contact", label: "Contact", icon: React.createElement(LucideReact.Mail, { className: "h-4 w-4" }) }),
                        React.createElement(NavLink, { to: "/login", label: "Login", icon: React.createElement(LucideReact.LogIn, { className: "h-4 w-4" }) }),
                        React.createElement('a', { href: BRAND.register, target: "_blank", rel: "noreferrer" },
                            React.createElement(Button, { className: "ml-2 rounded-2xl" }, "Register")
                        )
                    ),
                    React.createElement(Button, { variant: "ghost", className: "md:hidden", onClick: () => setOpen((v) => !v) },
                        React.createElement(LucideReact.AlignLeft, { className: "h-5 w-5" })
                    )
                ),
                open && React.createElement('div', { className: "md:hidden border-t border-white/10" },
                    React.createElement('div', { className: "mx-auto max-w-6xl px-4 py-2 grid gap-2" },
                        React.createElement(MobileNavLink, { to: "/", label: "Home" }),
                        React.createElement(MobileNavLink, { to: "/earn", label: "Ways to Earn" }),
                        React.createElement(MobileNavLink, { to: "/contact", label: "Contact" }),
                        React.createElement(MobileNavLink, { to: "/login", label: "Login" }),
                        React.createElement('a', { 
                            className: "rounded-xl bg-emerald-500/20 px-3 py-2 text-emerald-300", 
                            href: BRAND.register, 
                            target: "_blank", 
                            rel: "noreferrer" 
                        }, "Register")
                    )
                )
            ); 
        }

        function NavLink({ to, label, icon }) { 
            return React.createElement(Link, { to: to, className: "rounded-xl px-3 py-2 text-sm hover:bg-white/5" },
                React.createElement('span', { className: "inline-flex items-center gap-2 opacity-90 hover:opacity-100" }, icon, label)
            ); 
        } 

        function MobileNavLink({ to, label }) { 
            return React.createElement(Link, { to: to, className: "rounded-xl px-3 py-2 text-sm hover:bg-white/5" }, label); 
        }

        function Footer() { 
            return React.createElement('footer', { className: "border-t border-white/10" },
                React.createElement('div', { className: "mx-auto max-w-6xl px-4 py-10 grid gap-6 md:grid-cols-3" },
                    React.createElement('div', null,
                        React.createElement('div', { className: "flex items-center gap-2" },
                            React.createElement('div', { className: "h-8 w-8 rounded-xl bg-gradient-to-br from-emerald-400 to-cyan-400" }),
                            React.createElement('span', { className: "font-semibold" }, BRAND.name)
                        ),
                        React.createElement('p', { className: "mt-3 text-sm text-slate-300/80" }, "Your success partner! Earn online using your smartphone from anywhere you are.")
                    ),
                    React.createElement('div', { className: "text-sm" },
                        React.createElement('div', { className: "font-semibold mb-2" }, "Quick Links"),
                        React.createElement('ul', { className: "grid gap-1" },
                            React.createElement('li', null, React.createElement(Link, { className: "hover:underline", to: "/earn" }, "Ways to Earn")),
                            React.createElement('li', null, React.createElement('a', { className: "hover:underline", href: BRAND.register, target: "_blank", rel: "noreferrer" }, "Register")),
                            React.createElement('li', null, React.createElement(Link, { className: "hover:underline", to: "/login" }, "Login")),
                            React.createElement('li', null, React.createElement(Link, { className: "hover:underline", to: "/contact" }, "Contact"))
                        )
                    ),
                    React.createElement('div', { className: "text-sm" },
                        React.createElement('div', { className: "font-semibold mb-2" }, "Reach Us"),
                        React.createElement('div', { className: "flex flex-col gap-2" },
                            React.createElement('a', { className: "inline-flex items-center gap-2 hover:underline", href: BRAND.whatsapp, target: "_blank", rel: "noreferrer" },
                                React.createElement(LucideReact.Phone, { className: "h-4 w-4" }),
                                " WhatsApp"
                            ),
                            React.createElement('a', { className: "inline-flex items-center gap-2 hover:underline", href: BRAND.email },
                                React.createElement(LucideReact.Mail, { className: "h-4 w-4" }),
                                " teejaeyke@gmail.com"
                            )
                        )
                    )
                ),
                React.createElement('div', { className: "border-t border-white/10 py-4 text-center text-xs text-slate-500" },
                    `© ${new Date().getFullYear()} ${BRAND.name}. All rights reserved.`
                )
            ); 
        }

        function WhatsAppFAB() { 
            return React.createElement('a', { href: BRAND.whatsapp, target: "_blank", rel: "noreferrer", className: "fixed bottom-5 right-5 z-50" },
                React.createElement(Button, { size: "lg", className: "rounded-full shadow-lg" },
                    React.createElement(LucideReact.MessageSquare, { className: "mr-2 h-4 w-4" }),
                    "Chat on WhatsApp"
                )
            ); 
        }

        // ====== PAGES ====== 
        function Home() { 
            const perks = [ 
                { icon: React.createElement(LucideReact.ShieldCheck, { className: "h-5 w-5" }), title: "Activation $8", desc: "One-time activation to unlock the platform." }, 
                { icon: React.createElement(LucideReact.Rocket, { className: "h-5 w-5" }), title: "Up to $40+/day", desc: "With an active account and consistent effort." }, 
                { icon: React.createElement(LucideReact.Users2, { className: "h-5 w-5" }), title: "Affiliate Levels (3)", desc: "Level 1: $3 • Level 2: $1.5 • Level 3: $0.5" }, 
            ];

            return React.createElement(Shell, null,
                React.createElement('section', { className: "grid gap-10 md:grid-cols-2 md:items-center" },
                    React.createElement('div', null,
                        React.createElement(motion.h1, { 
                            initial: { opacity: 0, y: 12 }, 
                            animate: { opacity: 1, y: 0 }, 
                            transition: { duration: 0.5 }, 
                            className: "text-4xl font-bold leading-tight md:text-5xl" 
                        }, 
                            "Welcome to ",
                            React.createElement('span', { className: "bg-gradient-to-r from-emerald-400 to-cyan-400 bg-clip-text text-transparent" }, BRAND.name)
                        ),
                        React.createElement('p', { className: "mt-4 text-slate-300/90" }, 
                            "Your success partner! Earn online using your smartphone from the comfort of your home, school, or anywhere you are."
                        ),
                        React.createElement('div', { className: "mt-6 flex flex-wrap gap-3" },
                            React.createElement(Link, { to: "/earn" },
                                React.createElement(Button, { size: "lg", className: "rounded-2xl" },
                                    "Explore Ways to Earn ",
                                    React.createElement(LucideReact.ArrowRight, { className: "ml-2 h-4 w-4" })
                                )
                            ),
                            React.createElement('a', { href: BRAND.register, target: "_blank", rel: "noreferrer" },
                                React.createElement(Button, { size: "lg", variant: "secondary", className: "rounded-2xl" }, "Register Now")
                            )
                        ),
                        React.createElement('div', { className: "mt-6 flex flex-wrap gap-2" },
                            perks.map((p, i) => 
                                React.createElement(Badge, { key: i, className: "rounded-xl bg-white/5 px-3 py-1 text-slate-200" },
                                    React.createElement('span', { className: "mr-2 inline-flex" }, p.icon),
                                    p.title
                                )
                            )
                        )
                    ),
                    React.createElement(motion.div, { 
                        initial: { opacity: 0, scale: 0.95 }, 
                        animate: { opacity: 1, scale: 1 }, 
                        transition: { duration: 0.5, delay: 0.05 }, 
                        className: "grid gap-4" 
                    },
                        React.createElement(Card, { className: "rounded-2xl border-white/10 bg-white/5" },
                            React.createElement(CardHeader, null,
                                React.createElement(CardTitle, { className: "text-lg" }, "Highlights")
                            ),
                            React.createElement(CardContent, { className: "grid gap-3 text-sm text-slate-300/90" },
                                React.createElement('p', null, "✍🏼 Activation fee is ", React.createElement('span', { className: "font-semibold" }, "USD 8"), "."),
                                React.createElement('p', null, "⏰ With an active account, be ready to make up to ", React.createElement('span', { className: "font-semibold" }, "USD 40+ daily"), "."),
                                React.createElement('p', null, "🎯 Welcome bonus: ", React.createElement('span', { className: "font-semibold" }, "USD 1.5"), " after activation.")
                            )
                        ),
                        React.createElement(StatsStrip)
                    )
                ),
                React.createElement('section', { className: "mt-14" },
                    React.createElement(EarnGrid, { compact: true })
                )
            ); 
        }

        function StatsStrip() { 
            const stats = [ 
                { label: "Weekly agent bonus", icon: React.createElement(LucideReact.Wallet, { className: "h-4 w-4" }) }, 
                { label: "Automatic Activations", icon: React.createElement(LucideReact.CheckCircle2, { className: "h-4 w-4" }) }, 
                { label: "Instant withdrawals", icon: React.createElement(LucideReact.Loader2, { className: "h-4 w-4" }) }, 
                { label: "Free Forex classes", icon: React.createElement(LucideReact.PlaySquare, { className: "h-4 w-4" }) }, 
                { label: "24/7 customer service", icon: React.createElement(LucideReact.ThumbsUp, { className: "h-4 w-4" }) }, 
            ]; 
            return React.createElement('div', { className: "grid grid-cols-1 gap-2 sm:grid-cols-2 md:grid-cols-3" },
                stats.map((s, i) => 
                    React.createElement(Card, { key: i, className: "rounded-2xl border-white/10 bg-white/5" },
                        React.createElement(CardContent, { className: "flex items-center gap-2 p-4 text-sm text-slate-300/90" },
                            s.icon,
                            React.createElement('span', null, s.label)
                        )
                    )
                )
            ); 
        }

        function EarnGrid({ compact = false }) { 
            const items = useMemo(() => ([ 
                { icon: React.createElement(LucideReact.CheckCircle2, { className: "h-5 w-5" }), title: "Welcome Bonus", desc: "Get USD 1.5 immediately after activation." }, 
                { icon: React.createElement(LucideReact.AlignLeft, { className: "h-5 w-5" }), title: "Answer Surveys", desc: "Complete simple surveys and earn." }, 
                { icon: React.createElement(LucideReact.PlaySquare, { className: "h-5 w-5" }), title: "Watch YouTube", desc: "Watch promotional videos and earn." }, 
                { icon: React.createElement(LucideReact.PlaySquare, { className: "h-5 w-5" }), title: "Watch TikTok", desc: "Watch promotional TikTok videos and earn." }, 
                { icon: React.createElement(LucideReact.Gamepad2, { className: "h-5 w-5" }), title: "Play Games", desc: "Play games of your choice and earn." }, 
                { icon: React.createElement(LucideReact.ThumbsUp, { className: "h-5 w-5" }), title: "Click Ads", desc: "Click on ads and earn." }, 
                { icon: React.createElement(LucideReact.Instagram, { className: "h-5 w-5" }), title: "Watch IG Reels", desc: "Watch Instagram reels and earn." }, 
                { icon: React.createElement(LucideReact.Facebook, { className: "h-5 w-5" }), title: "Watch FB Reels", desc: "Watch Facebook reels and earn." }, 
                { icon: React.createElement(LucideReact.Users2, { className: "h-5 w-5" }), title: "Affiliate Program", desc: "Earn in 3 levels: L1 $3, L2 $1.5, L3 $0.5." }, 
            ]), []);

            return React.createElement('section', null,
                !compact && React.createElement('h2', { className: "mb-4 text-2xl font-semibold" }, "Ways of Earning"),
                React.createElement('div', { className: "grid grid-cols-1 gap-3 sm:grid-cols-2 md:grid-cols-3" },
                    items.map((it, i) => 
                        React.createElement(Card, { key: i, className: "rounded-2xl border-white/10 bg-white/5 hover:bg-white/10 transition" },
                            React.createElement(CardContent, { className: "p-4" },
                                React.createElement('div', { className: "flex items-center gap-2 text-emerald-300" },
                                    it.icon,
                                    React.createElement('span', { className: "font-medium text-slate-100" }, it.title)
                                ),
                                React.createElement('p', { className: "mt-2 text-sm text-slate-300/90" }, it.desc)
                            )
                        )
                    )
                )
            ); 
        }

        function EarnPage() { 
            return React.createElement(Shell, null,
                React.createElement('div', { className: "max-w-3xl" },
                    React.createElement('h1', { className: "text-3xl font-bold" }, "Ways of Earning"),
                    React.createElement('p', { className: "mt-3 text-slate-300/90" }, "🔰✋🏼 WELCOME TO HELALINK AGENCIES MAKE MONEY ONLINE 🌍 💭"),
                    React.createElement('p', { className: "mt-2 text-slate-300/90" }, "🔮 Your success partner! Earn online using your smartphone from the comfort of your home, place, school or from anywhere you are. 💫"),
                    React.createElement('div', { className: "mt-6" },
                        React.createElement(EarnGrid)
                    ),
                    React.createElement('div', { className: "mt-8 grid gap-3" },
                        React.createElement(Card, { className: "rounded-2xl border-white/10 bg-white/5" },
                            React.createElement(CardHeader, null,
                                React.createElement(CardTitle, null, "Affiliate Levels")
                            ),
                            React.createElement(CardContent, { className: "text-sm text-slate-300/90" },
                                "Level 1 ➡️ USD 3",
                                React.createElement('br'),
                                "Level 2 ➡️ USD 1.5",
                                React.createElement('br'),
                                "Level 3 ➡️ USD 0.5"
                            )
                        ),
                        React.createElement(Card, { className: "rounded-2xl border-white/10 bg-white/5" },
                            React.createElement(CardHeader, null,
                                React.createElement(CardTitle, null, "Added Advantages")
                            ),
                            React.createElement(CardContent, { className: "text-sm text-slate-300/90 grid gap-1" },
                                React.createElement('div', null, "🥎 Weekly agent bonus"),
                                React.createElement('div', null, "🥎 Automatic Activations"),
                                React.createElement('div', null, "🥎 Instant withdrawals"),
                                React.createElement('div', null, "🎾 Free Forex classes"),
                                React.createElement('div', null, "🥎 24/7 customer service")
                            )
                        )
                    ),
                    React.createElement('div', { className: "mt-10 flex flex-wrap gap-3" },
                        React.createElement('a', { href: BRAND.register, target: "_blank", rel: "noreferrer" },
                            React.createElement(Button, { size: "lg", className: "rounded-2xl" }, "Register Now")
                        ),
                        React.createElement('a', { href: BRAND.whatsapp, target: "_blank", rel: "noreferrer" },
                            React.createElement(Button, { variant: "secondary", size: "lg", className: "rounded-2xl" }, "Chat on WhatsApp")
                        )
                    )
                )
            ); 
        }

        function ContactPage() { 
            const [form, setForm] = useState({ name: "", email: "", message: "" }); 
            const [sent, setSent] = useState(false);

            const onSubmit = (e) => { 
                e.preventDefault(); 
                // OPEN default mail client with prefilled details (no backend needed) 
                const subject = encodeURIComponent(`Inquiry from ${form.name}`); 
                const body = encodeURIComponent(`Name: ${form.name}\nEmail: ${form.email}\n\n${form.message}`); 
                window.location.href = `${BRAND.email}?subject=${subject}&body=${body}`; 
                setSent(true); 
            };

            return React.createElement(Shell, null,
                React.createElement('div', { className: "max-w-xl" },
                    React.createElement('h1', { className: "text-3xl font-bold" }, "Contact Us"),
                    React.createElement('p', { className: "mt-2 text-slate-300/90" }, "Have questions? Send us a message and we'll get back to you."),
                    React.createElement('form', { onSubmit: onSubmit, className: "mt-6 grid gap-4" },
                        React.createElement('div', null,
                            React.createElement('label', { className: "mb-1 block text-sm text-slate-300" }, "Your Name"),
                            React.createElement(Input, { 
                                required: true,
                                value: form.name, 
                                onChange: (e) => setForm({ ...form, name: e.target.value }), 
                                placeholder: "Jane Doe", 
                                className: "bg-white/5" 
                            })
                        ),
                        React.createElement('div', null,
                            React.createElement('label', { className: "mb-1 block text-sm text-slate-300" }, "Email"),
                            React.createElement(Input, { 
                                required: true,
                                type: "email", 
                                value: form.email, 
                                onChange: (e) => setForm({ ...form, email: e.target.value }), 
                                placeholder: "you@example.com", 
                                className: "bg-white/5" 
                            })
                        ),
                        React.createElement('div', null,
                            React.createElement('label', { className: "mb-1 block text-sm text-slate-300" }, "Message"),
                            React.createElement(Textarea, { 
                                required: true,
                                value: form.message, 
                                onChange: (e) => setForm({ ...form, message: e.target.value }), 
                                placeholder: "How can we help?", 
                                className: "bg-white/5" 
                            })
                        ),
                        React.createElement('div', { className: "flex items-center gap-3" },
                            React.createElement(Button, { type: "submit", className: "rounded-2xl" }, "Send Message"),
                            React.createElement('a', { href: BRAND.whatsapp, target: "_blank", rel: "noreferrer" },
                                React.createElement(Button, { variant: "secondary", type: "button", className: "rounded-2xl" }, "WhatsApp")
                            )
                        ),
                        sent && React.createElement('p', { className: "text-sm text-emerald-300" }, "Thanks! Your email draft opened in your mail app.")
                    )
                )
            ); 
        }

        function LoginPage() { 
            const [creds, setCreds] = useState({ email: "", password: "" }); 
            const [error, setError] = useState(""); 
            const nav = useNavigate();

            const handleLogin = (e) => { 
                e.preventDefault(); 
                setError(""); 
                // Demo client-side login. In production, replace with real auth API. 
                if (creds.email && creds.password.length >= 4) { 
                    localStorage.setItem("hl_auth", JSON.stringify({ email: creds.email, ts: Date.now() })); 
                    nav("/dashboard"); 
                } else { 
                    setError("Invalid email or password"); 
                } 
            };

            return React.createElement(Shell, null,
                React.createElement('div', { className: "mx-auto w-full max-w-sm" },
                    React.createElement('h1', { className: "text-3xl font-bold" }, "Login"),
                    React.createElement('p', { className: "mt-2 text-slate-300/90" }, "Use your email and password to continue."),
                    React.createElement('form', { onSubmit: handleLogin, className: "mt-6 grid gap-4" },
                        React.createElement('div', null,
                            React.createElement('label', { className: "mb-1 block text-sm text-slate-300" }, "Email"),
                            React.createElement(Input, { 
                                type: "email", 
                                required: true,
                                value: creds.email, 
                                onChange: (e) => setCreds({ ...creds, email: e.target.value }), 
                                placeholder: "you@example.com", 
                                className: "bg-white/5" 
                            })
                        ),
                        React.createElement('div', null,
                            React.createElement('label', { className: "mb-1 block text-sm text-slate-300" }, "Password"),
                            React.createElement(Input, { 
                                type: "password", 
                                required: true,
                                value: creds.password, 
                                onChange: (e) => setCreds({ ...creds, password: e.target.value }), 
                                placeholder: "••••••••", 
                                className: "bg-white/5" 
                            })
                        ),
                        error && React.createElement('p', { className: "text-sm text-rose-300" }, error),
                        React.createElement(Button, { type: "submit", className: "rounded-2xl" },
                            React.createElement(LucideReact.LogIn, { className: "mr-2 h-4 w-4" }),
                            " Login"
                        ),
                        React.createElement('a', { 
                            href: BRAND.register, 
                            target: "_blank", 
                            rel: "noreferrer", 
                            className: "text-center text-sm text-emerald-300 hover:underline" 
                        }, "Don't have an account? Register")
                    )
                )
            ); 
        }

        function Dashboard() { 
            const nav = useNavigate(); 
            const [user, setUser] = useState(null); 
            useEffect(() => { 
                const raw = localStorage.getItem("hl_auth"); 
                if (!raw) return nav("/login"); 
                setUser(JSON.parse(raw)); 
            }, [nav]);

            const logout = () => { 
                localStorage.removeItem("hl_auth"); 
                nav("/login"); 
            };

            if (!user) return React.createElement(Shell, null,
                React.createElement('div', { className: "py-20 text-center text-slate-300" }, "Loading…")
            );

            return React.createElement(Shell, null,
                React.createElement('div', { className: "grid gap-6" },
                    React.createElement('div', { className: "flex flex-wrap items-center justify-between gap-3" },
                        React.createElement('h1', { className: "text-3xl font-bold" }, `Welcome, ${user.email}`),
                        React.createElement('div', { className: "flex gap-2" },
                            React.createElement(Link, { to: "/earn" },
                                React.createElement(Button, { variant: "secondary", className: "rounded-2xl" }, "View Earning Options")
                            ),
                            React.createElement(Button, { onClick: logout, className: "rounded-2xl" }, "Logout")
                        )
                    ),
                    React.createElement('div', { className: "grid grid-cols-1 gap-4 md:grid-cols-3" },
                        React.createElement(Card, { className: "rounded-2xl border-white/10 bg-white/5" },
                            React.createElement(CardHeader, null,
                                React.createElement(CardTitle, null, "Account")
                            ),
                            React.createElement(CardContent, { className: "text-sm text-slate-300/90" },
                                "Status: ",
                                React.createElement('span', { className: "text-emerald-300" }, "Active (demo)"),
                                React.createElement('br'),
                                "Activation Fee: USD 8"
                            )
                        ),
                        React.createElement(Card, { className: "rounded-2xl border-white/10 bg-white/5" },
                            React.createElement(CardHeader, null,
                                React.createElement(CardTitle, null, "Potential Earnings")
                            ),
                            React.createElement(CardContent, { className: "text-sm text-slate-300/90" }, "Up to USD 40+/day with activity.")
                        ),
                        React.createElement(Card, { className: "rounded-2xl border-white/10 bg-white/5" },
                            React.createElement(CardHeader, null,
                                React.createElement(CardTitle, null, "Affiliate Levels")
                            ),
                            React.createElement(CardContent, { className: "text-sm text-slate-300/90" }, "L1 $3 • L2 $1.5 • L3 $0.5")
                        )
                    ),
                    React.createElement(Card, { className: "rounded-2xl border-white/10 bg-white/5" },
                        React.createElement(CardHeader, null,
                            React.createElement(CardTitle, null, "Get Started")
                        ),
                        React.createElement(CardContent, { className: "text-sm text-slate-300/90" },
                            React.createElement('ol', { className: "list-decimal pl-5" },
                                React.createElement('li', null,
                                    "Register your account: ",
                                    React.createElement('a', { 
                                        className: "text-emerald-300 hover:underline", 
                                        href: BRAND.register, 
                                        target: "_blank", 
                                        rel: "noreferrer" 
                                    }, "Registration Link")
                                ),
                                React.createElement('li', null,
                                    "Chat with us on WhatsApp if you need help: ",
                                    React.createElement('a', { 
                                        className: "text-emerald-300 hover:underline", 
                                        href: BRAND.whatsapp, 
                                        target: "_blank", 
                                        rel: "noreferrer" 
                                    }, "Open WhatsApp")
                                ),
                                React.createElement('li', null,
                                    "Explore earning options inside ",
                                    React.createElement(Link, { 
                                        to: "/earn", 
                                        className: "text-emerald-300 hover:underline" 
                                    }, "Ways to Earn"),
                                    "."
                                )
                            )
                        )
                    )
                )
            ); 
        }

        // ====== APP (ROUTER) ====== 
        function App() { 
            return React.createElement(BrowserRouter, null,
                React.createElement(Routes, null,
                    React.createElement(Route, { path: "/", element: React.createElement(Home) }),
                    React.createElement(Route, { path: "/earn", element: React.createElement(EarnPage) }),
                    React.createElement(Route, { path: "/contact", element: React.createElement(ContactPage) }),
                    React.createElement(Route, { path: "/login", element: React.createElement(LoginPage) }),
                    React.createElement(Route, { path: "/dashboard", element: React.createElement(Dashboard) })
                )
            ); 
        }

        // Render the app
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(React.createElement(App));
    </script>
</body>
</html>in
