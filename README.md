# shed-at-dulwich

import React, { useMemo, useState } from "react";
import { motion } from "framer-motion";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { Label } from "@/components/ui/label";
import { Select, SelectTrigger, SelectContent, SelectValue, SelectItem } from "@/components/ui/select";
import { CalendarDays, Leaf, Phone, Mail, MapPin, Clock, Star, Utensils } from "lucide-react";

// ------------------------------------------------------------
// THE SHED AT DULWICH — SINGLE-FILE REACT SITE
// - TailwindCSS styling
// - shadcn/ui components
// - Framer Motion animations
// - Fully vegetarian Western menu with vegan symbols
// - "10 seatings per day" message + pre-order reservation form
// ------------------------------------------------------------

const VEG = "🟩"; // Vegetarian symbol
const VEGAN = "🌱"; // Vegan symbol

const menuData = {
  amuse: [
    { name: "Heirloom Tomato Essence", desc: "Infused tomato consommé with basil foam", tag: VEGAN },
    { name: "Truffle-Infused Polenta Crisp", desc: "Delicate crisps with black truffle oil & edible flowers", tag: VEGAN },
  ],
  appetizers: [
    { name: "Charred Asparagus & Walnut Pâté", desc: "Sourdough croustade, lemon-zest microgreens", tag: VEGAN },
    { name: "Pumpkin Velouté", desc: "Roasted pumpkin soup, coconut cream, almond dust", tag: VEGAN },
    { name: "Beetroot Carpaccio", desc: "Balsamic glaze, candied pecans, goat-cheese crumble", tag: VEG },
  ],
  mains: [
    { name: "Wild Mushroom Risotto", desc: "Arborio, forest mushrooms, parmesan, truffle oil", tag: VEG },
    { name: "Stuffed Bell Peppers", desc: "Couscous & herbs, tomato–caper reduction, pine nuts", tag: VEGAN },
    { name: "Aubergine Mille‑Feuille", desc: "Roasted eggplant layers, ricotta, basil", tag: VEG },
    { name: "Vegan Shepherd’s Pie", desc: "Lentil, carrot & mushroom ragout, garlic mash", tag: VEGAN },
  ],
  desserts: [
    { name: "Dark Chocolate Avocado Mousse", desc: "70% Belgian chocolate, coconut cream, pistachio brittle", tag: VEGAN },
    { name: "Panna Cotta", desc: "Vanilla bean, raspberry & blueberry compote", tag: VEG },
    { name: "Vegan Tiramisu in a Jar", desc: "Espresso-soaked sponge, cashew mascarpone, cacao dust", tag: VEGAN },
  ],
  beverages: [
    { name: "Cucumber–Mint Sparkle", desc: "Crisp, refreshing, house carbonated", tag: VEGAN },
    { name: "Charcoal Lemonade", desc: "Activated charcoal, Himalayan salt", tag: VEGAN },
    { name: "Elderflower Citrus Punch", desc: "Elderflower, orange, lime, gently sweet", tag: VEGAN },
    { name: "Organic Herbal Tea Selection", desc: "Chamomile, peppermint, lemongrass", tag: VEGAN },
  ],
};

function SectionTitle({ icon: Icon, overline, title, subtitle }) {
  return (
    <div className="text-center space-y-2 mb-8">
      <div className="text-xs tracking-widest uppercase text-muted-foreground">{overline}</div>
      <div className="flex items-center justify-center gap-2">
        {Icon && <Icon className="w-5 h-5" />}
        <h2 className="text-2xl sm:text-3xl font-semibold">{title}</h2>
      </div>
      {subtitle && <p className="text-muted-foreground max-w-2xl mx-auto">{subtitle}</p>}
    </div>
  );
}

function MenuSection({ heading, items }) {
  return (
    <div className="grid gap-4 sm:grid-cols-2">
      {items.map((m, i) => (
        <Card key={i} className="rounded-2xl border-muted/40">
          <CardHeader>
            <CardTitle className="flex items-center justify-between gap-3 text-lg">
              <span className="font-medium">{m.name}</span>
              <span className="text-xl" title={m.tag === VEGAN ? "Vegan" : "Vegetarian"}>{m.tag}</span>
            </CardTitle>
          </CardHeader>
          <CardContent>
            <p className="text-muted-foreground leading-relaxed">{m.desc}</p>
          </CardContent>
        </Card>
      ))}
    </div>
  );
}

export default function ShedAtDulwichSite() {
  const [form, setForm] = useState({ date: "", time: "", seats: "2", name: "", phone: "", email: "", notes: "" });
  const todayISO = useMemo(() => new Date().toISOString().split("T")[0], []);

  function handleSubmit(e) {
    e.preventDefault();
    const details = `Reservation Request\nName: ${form.name}\nPhone: ${form.phone}\nEmail: ${form.email}\nDate: ${form.date}\nTime: ${form.time}\nGuests: ${form.seats}\nNotes: ${form.notes}`;
    alert(details + "\n\nThank you! This is a demo form. We will confirm availability (max 10 seatings/day)." );
  }

  return (
    <div className="min-h-screen bg-gradient-to-b from-amber-50 to-white text-slate-900">
      {/* NAVBAR */}
      <header className="sticky top-0 z-50 backdrop-blur bg-white/60 border-b border-amber-100">
        <div className="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="w-9 h-9 rounded-2xl bg-emerald-600 flex items-center justify-center shadow-sm">
              <Leaf className="w-5 h-5 text-white" />
            </div>
            <div>
              <div className="font-semibold tracking-wide">The Shed at Dulwich</div>
              <div className="text-xs uppercase tracking-widest text-muted-foreground">Top Roof Restaurant</div>
            </div>
          </div>
          <nav className="hidden md:flex items-center gap-6 text-sm">
            <a href="#about" className="hover:text-emerald-700">About</a>
            <a href="#menu" className="hover:text-emerald-700">Menu</a>
            <a href="#reserve" className="hover:text-emerald-700">Reserve</a>
            <a href="#contact" className="hover:text-emerald-700">Contact</a>
          </nav>
          <Button asChild className="rounded-2xl">
            <a href="#reserve" className="flex items-center gap-2"><CalendarDays className="w-4 h-4"/> Pre‑Order</a>
          </Button>
        </div>
      </header>

      {/* HERO */}
      <section className="relative overflow-hidden">
        <div className="max-w-6xl mx-auto px-4 py-20 sm:py-28">
          <motion.div initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.6 }} className="grid lg:grid-cols-2 gap-10 items-center">
            <div className="space-y-6">
              <span className="text-xs tracking-widest uppercase text-emerald-700">Gourmet Vegetarian Western Dining</span>
              <h1 className="font-serif text-4xl sm:text-5xl leading-tight">Elevated, <span className="text-emerald-700">Plant‑Forward</span> Cuisine on a Rooftop</h1>
              <p className="text-muted-foreground max-w-xl">Ten exclusive seatings per day. Pre‑order only. A seasonal tasting of modern Western classics—crafted entirely vegetarian with clear vegan options.</p>
              <div className="flex gap-3">
                <Button asChild size="lg" className="rounded-2xl"><a href="#menu"><Utensils className="w-4 h-4 mr-2"/> View Menu</a></Button>
                <Button asChild size="lg" variant="outline" className="rounded-2xl"><a href="#reserve"><CalendarDays className="w-4 h-4 mr-2"/> Reserve</a></Button>
              </div>
              <div className="flex items-center gap-4 text-sm text-muted-foreground">
                <div className="flex items-center gap-1"><Star className="w-4 h-4"/> Five‑Star Presentation</div>
                <div className="flex items-center gap-1"><Clock className="w-4 h-4"/> Pre‑Order Required</div>
              </div>
            </div>
            <motion.div initial={{ scale: 0.98, opacity: 0 }} animate={{ scale: 1, opacity: 1 }} transition={{ delay: 0.15, duration: 0.6 }} className="bg-[url('https://images.unsplash.com/photo-1544025162-d76694265947?q=80&w=2070&auto=format&fit=crop')] bg-cover bg-center rounded-3xl h-80 shadow-[0_20px_60px_-15px_rgba(16,185,129,0.35)]"/>
          </motion.div>
        </div>
      </section>

      {/* ABOUT */}
      <section id="about" className="py-16 sm:py-24">
        <div className="max-w-6xl mx-auto px-4">
          <SectionTitle icon={Leaf} overline="About" title="Sustainably Luxurious" subtitle="We cook with seasonal produce, artisanal cheeses, and house-fermented accents—always 100% vegetarian with clearly marked vegan options." />
          <div className="grid md:grid-cols-3 gap-6">
            {["10 seatings per day", "Pre‑order tasting", "Rooftop ambience"].map((t, i) => (
              <Card key={i} className="rounded-2xl border-emerald-100">
                <CardContent className="p-6 text-center text-sm">
                  <div className="text-3xl mb-2">{i===0?"10":i===1?"🗒️":"🌆"}</div>
                  <div className="font-medium">{t}</div>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* MENU */}
      <section id="menu" className="py-16 sm:py-24 bg-emerald-50/50">
        <div className="max-w-6xl mx-auto px-4">
          <SectionTitle icon={Utensils} overline="Menu" title="Five‑Star Vegetarian Menu" subtitle={`${VEGAN} Vegan | ${VEG} Contains Dairy`} />

          <div className="space-y-12">
            <div>
              <h3 className="text-xl font-semibold mb-4">Amuse‑Bouche</h3>
              <MenuSection items={menuData.amuse} />
            </div>
            <div>
              <h3 className="text-xl font-semibold mb-4">Appetizers</h3>
              <MenuSection items={menuData.appetizers} />
            </div>
            <div>
              <h3 className="text-xl font-semibold mb-4">Mains</h3>
              <MenuSection items={menuData.mains} />
            </div>
            <div>
              <h3 className="text-xl font-semibold mb-4">Desserts</h3>
              <MenuSection items={menuData.desserts} />
            </div>
            <div>
              <h3 className="text-xl font-semibold mb-4">Beverages & Mocktails</h3>
              <MenuSection items={menuData.beverages} />
            </div>
          </div>

          <p className="text-xs text-muted-foreground mt-8">Note: No onion/garlic dishes available on request. Our kitchen handles dairy and nuts.</p>
        </div>
      </section>

      {/* RESERVATION */}
      <section id="reserve" className="py-16 sm:py-24">
        <div className="max-w-6xl mx-auto px-4">
          <SectionTitle icon={CalendarDays} overline="Reservations" title="Pre‑Order Your Experience" subtitle="We accept a maximum of 10 seatings per day. Your reservation is confirmed only after our concierge contacts you." />

          <div className="grid lg:grid-cols-5 gap-8">
            <Card className="rounded-2xl lg:col-span-3">
              <CardHeader>
                <CardTitle>Reservation Request Form</CardTitle>
              </CardHeader>
              <CardContent>
                <form onSubmit={handleSubmit} className="grid gap-4">
                  <div className="grid sm:grid-cols-2 gap-4">
                    <div>
                      <Label htmlFor="date">Date</Label>
                      <Input id="date" type="date" min={todayISO} value={form.date} onChange={e=>setForm(f=>({...f, date:e.target.value}))} required />
                    </div>
                    <div>
                      <Label htmlFor="time">Time</Label>
                      <Input id="time" type="time" value={form.time} onChange={e=>setForm(f=>({...f, time:e.target.value}))} required />
                    </div>
                  </div>

                  <div className="grid sm:grid-cols-3 gap-4">
                    <div>
                      <Label>Guests</Label>
                      <Select value={form.seats} onValueChange={(v)=>setForm(f=>({...f, seats:v}))}>
                        <SelectTrigger><SelectValue placeholder="Guests"/></SelectTrigger>
                        <SelectContent>
                          {["1","2","3","4","5","6"].map(v=> (
                            <SelectItem key={v} value={v}>{v}</SelectItem>
                          ))}
                        </SelectContent>
                      </Select>
                    </div>
                    <div className="sm:col-span-2">
                      <Label htmlFor="name">Full Name</Label>
                      <Input id="name" value={form.name} onChange={e=>setForm(f=>({...f, name:e.target.value}))} required />
                    </div>
                  </div>

                  <div className="grid sm:grid-cols-2 gap-4">
                    <div>
                      <Label htmlFor="phone">Phone</Label>
                      <Input id="phone" type="tel" value={form.phone} onChange={e=>setForm(f=>({...f, phone:e.target.value}))} required />
                    </div>
                    <div>
                      <Label htmlFor="email">Email</Label>
                      <Input id="email" type="email" value={form.email} onChange={e=>setForm(f=>({...f, email:e.target.value}))} required />
                    </div>
                  </div>

                  <div>
                    <Label htmlFor="notes">Pre‑Order Notes (dietary, dish selections, no onion/garlic, etc.)</Label>
                    <Textarea id="notes" rows={4} value={form.notes} onChange={e=>setForm(f=>({...f, notes:e.target.value}))} placeholder="List preferred dishes and any dietary preferences here." />
                  </div>

                  <Button type="submit" size="lg" className="rounded-2xl">Submit Pre‑Order</Button>
                </form>
              </CardContent>
            </Card>

            <div className="lg:col-span-2 space-y-4">
              <Card className="rounded-2xl">
                <CardHeader>
                  <CardTitle className="flex items-center gap-2"><Clock className="w-4 h-4"/> Service Windows</CardTitle>
                </CardHeader>
                <CardContent className="text-sm text-muted-foreground">
                  <ul className="list-disc pl-5 space-y-1">
                    <li>Lunch: 12:30 – 14:30</li>
                    <li>Dinner: 19:00 – 21:30</li>
                    <li>Closed on Mondays</li>
                  </ul>
                </CardContent>
              </Card>
              <Card className="rounded-2xl">
                <CardHeader>
                  <CardTitle className="flex items-center gap-2"><MapPin className="w-4 h-4"/> Rooftop Location</CardTitle>
                </CardHeader>
                <CardContent className="text-sm text-muted-foreground">
                  <p>Exact address shared upon confirmation. Valet assistance available on request.</p>
                </CardContent>
              </Card>
              <Card className="rounded-2xl">
                <CardHeader>
                  <CardTitle className="flex items-center gap-2"><Phone className="w-4 h-4"/> Concierge</CardTitle>
                </CardHeader>
                <CardContent className="text-sm text-muted-foreground">
                  <p>+91‑XXXXXXXXXX • reservations@shedatdulwich.in</p>
                </CardContent>
              </Card>
            </div>
          </div>
        </div>
      </section>

      {/* FOOTER */}
      <footer id="contact" className="border-t bg-white/70">
        <div className="max-w-6xl mx-auto px-4 py-10 grid md:grid-cols-3 gap-8 text-sm">
          <div>
            <div className="font-semibold">The Shed at Dulwich</div>
            <div className="text-xs uppercase tracking-widest text-muted-foreground mb-2">Top Roof Restaurant</div>
            <p className="text-muted-foreground">A modern vegetarian Western experience. {VEGAN}=Vegan • {VEG}=Contains Dairy.</p>
          </div>
          <div>
            <div className="font-medium mb-2">Guest Policies</div>
            <ul className="space-y-1 text-muted-foreground">
              <li>Pre‑order required 24–72 hours in advance</li>
              <li>Max 10 seatings per day</li>
              <li>No onion/garlic on request • Nut kitchen</li>
            </ul>
          </div>
          <div>
            <div className="font-medium mb-2">Contact</div>
            <ul className="space-y-1 text-muted-foreground">
              <li className="flex items-center gap-2"><Phone className="w-4 h-4"/> +91‑XXXXXXXXXX</li>
              <li className="flex items-center gap-2"><Mail className="w-4 h-4"/> reservations@shedatdulwich.in</li>
              <li className="flex items-center gap-2"><MapPin className="w-4 h-4"/> Rooftop • Address on confirmation</li>
            </ul>
          </div>
        </div>
        <div className="text-center text-xs text-muted-foreground pb-8">© {new Date().getFullYear()} The Shed at Dulwich – All rights reserved.</div>
      </footer>
    </div>
  );
}
