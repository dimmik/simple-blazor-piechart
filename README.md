# Simple Blazor Pie Chart

Usage:
```
@page "/"
@using SimpleBlazorPieChart
@using ColorSequenceGenerator
@using Radzen.Blazor
<h1>Pie Chart Usage Examples</h1>
<h2>Pie Chart Default</h2>
<SimplePieChart 
    Data=@(
        new[] { 
            ("Product Licenses", 5000), 
            ("Consulting", 12000), 
            ("Audit", 8000), 
            ("Employee Salary", 15000) })
    />
<h2>Pie Chart no text</h2>
<SimplePieChart Data=@(
                new[] {
                ("Product Licenses", 5000),
                ("Consulting", 12000),
                ("Audit", 8000),
                ("Employee Salary", 15000) })
                ShowText=@false
    />

<h2>Pie Chart with additional controls</h2>
<SimplePieChart Data=@(
                new[] {
                ("Product Licenses", 5000),
                ("Consulting", 12000),
                ("Audit", 8000),
                ("Employee Salary", 15000) })
                ColorSequenceGenerator="csg"
>
    <ExtraControls>
        Current Seed color: <span style="color: @csg.Seed">@csg.Seed</span>
        @{
            if (Magic == -1) Magic = (int)(csg.Magic * 1000);
            if (Seed == null) Seed = csg.Seed;
        }
        <RadzenNumeric Min="1000" Max="5000" Step="1" Style="margin:0 16px;" @bind-Value="@Magic"
                               TValue="int"
                               Change=@(i => csg.Magic = Magic * 1.0 / 1000)
                                />
        <RadzenColorPicker @bind-Value=@Seed 
        Change=@(c => csg.Seed = Seed)/>
    </ExtraControls>
</SimplePieChart>

@code {
    private int Magic = -1;
    private string Seed = null;
    private CSG csg = new();
}
```