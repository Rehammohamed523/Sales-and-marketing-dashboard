# Sales-and-marketing-dashboard
The dashboard presents overall sales performance from 2022–2024, showing:  Revenue: 2M | Cost: 1M | Profit: 354K  Sales Channels: In-Store (67%) and Online (33%)  Top Countries: Japan leads in revenue (219K), followed by Germany and Canada.  Monthly Trend: Revenue fluctuates, with peaks in July and September and dips in April and June.  
import React from "react";
import {
  LineChart,
  Line,
  XAxis,
  YAxis,
  Tooltip,
  ResponsiveContainer,
  PieChart,
  Pie,
  Cell,
  Legend,
} from "recharts";
import { ArrowUpRight, ArrowDown } from "lucide-react";

// Single-file React component ready for a Create React App / Vite + Tailwind project
// Dependencies: react, react-dom, recharts, lucide-react, tailwindcss

const monthlyData = [
  { month: "Jan", revenue: 140000, revenue_pv: 80000 },
  { month: "Feb", revenue: 170000, revenue_pv: 70000 },
  { month: "Mar", revenue: 120000, revenue_pv: 60000 },
  { month: "Apr", revenue: 90000, revenue_pv: 30000 },
  { month: "May", revenue: 130000, revenue_pv: 40000 },
  { month: "Jun", revenue: 110000, revenue_pv: 35000 },
  { month: "Jul", revenue: 180000, revenue_pv: 90000 },
  { month: "Aug", revenue: 160000, revenue_pv: 60000 },
  { month: "Sep", revenue: 190000, revenue_pv: 110000 },
  { month: "Oct", revenue: 150000, revenue_pv: 80000 },
  { month: "Nov", revenue: 120000, revenue_pv: 70000 },
  { month: "Dec", revenue: 100000, revenue_pv: 50000 },
];

const channelData = [
  { name: "In-Store", value: 67.14 },
  { name: "Online", value: 32.86 },
];
const COLORS = ["#1E3A8A", "#60A5FA"];

const countries = [
  {
    flag: "🇯🇵",
    country: "Japan",
    profit: 49421,
    profit_growth: "100%",
    revenue: 219071,
    revenue_growth: "100%",
    coast: 169650,
  },
  {
    flag: "🇩🇪",
    country: "Germany",
    profit: 42432,
    profit_growth: "100%",
    revenue: 202530,
    revenue_growth: "100%",
    coast: 160098,
  },
  {
    flag: "🇨🇦",
    country: "Canada",
    profit: 46247,
    profit_growth: "100%",
    revenue: 216794,
    revenue_growth: "100%",
    coast: 170547,
  },
  {
    flag: "🇫🇷",
    country: "France",
    profit: 41283,
    profit_growth: "100%",
    revenue: 194538,
    revenue_growth: "100%",
    coast: 153255,
  },
  {
    flag: "🇧🇷",
    country: "Brazil",
    profit: 44196,
    profit_growth: "100%",
    revenue: 198086,
    revenue_growth: "100%",
    coast: 153890,
  },
];

export default function SalesDashboard() {
  const totalRevenue = "2M";
  const totalCost = "1M";
  const totalProfit = "354K";

  return (
    <div className="min-h-screen bg-sky-100 p-6 font-sans">
      <div className="max-w-6xl mx-auto">
        <header className="flex items-center justify-between mb-6">
          <h1 className="text-3xl font-bold text-white bg-sky-600 px-4 py-2 rounded-lg">
            Sales Dashboard
          </h1>
          <div className="flex gap-3">
            <button className="px-4 py-2 bg-white rounded-full shadow">2022</button>
            <button className="px-4 py-2 bg-white rounded-full shadow">2023</button>
            <button className="px-4 py-2 bg-white rounded-full shadow">2024</button>
          </div>
        </header>

        {/* KPI cards */}
        <div className="grid grid-cols-3 gap-4 mb-6">
          <Card title="profit" value={totalProfit} icon={<ArrowDown />} />
          <Card title="cost" value={totalCost} icon={<ArrowUpRight />} />
          <Card title="revenue" value={totalRevenue} icon={<ArrowUpRight />} />
        </div>

        <div className="grid grid-cols-3 gap-6">
          <div className="col-span-2 bg-white p-4 rounded-lg shadow">
            <h3 className="font-semibold mb-3">Revenue by Sales Channel</h3>
            <div style={{ height: 220 }}>
              <ResponsiveContainer>
                <PieChart>
                  <Pie
                    dataKey="value"
                    data={channelData}
                    cx="50%"
                    cy="50%"
                    outerRadius={80}
                    label
                  >
                    {channelData.map((entry, index) => (
                      <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                    ))}
                  </Pie>
                  <Legend />
                </PieChart>
              </ResponsiveContainer>
            </div>

            <div className="mt-6">
              <h3 className="font-semibold mb-3">Revenue and PV by Month</h3>
              <div style={{ height: 260 }}>
                <ResponsiveContainer>
                  <LineChart data={monthlyData}>
                    <XAxis dataKey="month" />
                    <YAxis />
                    <Tooltip />
                    <Line type="monotone" dataKey="revenue" stroke="#1E40AF" strokeWidth={2} />
                    <Line type="monotone" dataKey="revenue_pv" stroke="#1E3A8A" strokeWidth={2} />
                  </LineChart>
                </ResponsiveContainer>
              </div>
            </div>
          </div>

          <div className="bg-white p-4 rounded-lg shadow">
            <h3 className="font-semibold mb-3">Top Countries</h3>
            <div className="overflow-auto max-h-[520px]">
              <table className="w-full text-sm table-auto">
                <thead>
                  <tr className="bg-sky-50">
                    <th className="p-2 text-left">Flag</th>
                    <th className="p-2 text-left">Country</th>
                    <th className="p-2 text-right">Profit</th>
                    <th className="p-2 text-right">Profit Growth</th>
                    <th className="p-2 text-right">Revenue</th>
                    <th className="p-2 text-right">Revenue Growth</th>
                    <th className="p-2 text-right">Cost</th>
                  </tr>
                </thead>
                <tbody>
                  {countries.map((c) => (
                    <tr key={c.country} className="border-b">
                      <td className="p-2">{c.flag}</td>
                      <td className="p-2">{c.country}</td>
                      <td className="p-2 text-right">{c.profit.toLocaleString()}</td>
                      <td className="p-2 text-right">{c.profit_growth}</td>
                      <td className="p-2 text-right">{c.revenue.toLocaleString()}</td>
                      <td className="p-2 text-right">{c.revenue_growth}</td>
                      <td className="p-2 text-right">{c.coast.toLocaleString()}</td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <footer className="mt-6 text-xs text-gray-600">Generated dashboard demo • Replace sample data with your real dataset</footer>
      </div>
    </div>
  );
}

function Card({ title, value, icon }) {
  return (
    <div className="bg-white p-6 rounded-lg shadow flex items-center justify-between">
      <div>
        <div className="text-xs text-gray-500 uppercase">{title}</div>
        <div className="text-2xl font-bold">{value}</div>
      </div>
      <div className="text-3xl text-sky-600">{icon}</div>
    </div>
  );
}
