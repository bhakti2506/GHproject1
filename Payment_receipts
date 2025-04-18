from reportlab.platypus import TableStyle, SimpleDocTemplate, Table, Paragraph
from reportlab.lib import colors
from reportlab.lib.pagesizes import A4
from reportlab.lib.styles import getSampleStyleSheet
from reportlab.lib.units import cm

# Get user entries
entries = []

print("Enter subscription entries (leave name empty to stop):")
while True:
    date = input("Date (dd-mm-yy): ")
    name = input("Service Name: ")
    if name.strip() == "":
        break
    sub_type = input("Subscription Type (monthly/yearly): ")
    price = input("Price: ")
    entries.append([date, name, sub_type, price])

# Initial Header
DATA = [
    ["Date", "Name", "Subscription", "Price"]
]
DATA.extend(entries)

# Dynamic entries you want to add
# entries = [
#     ["18-04-25", "Youtube", "Yearly", "399"],
#     ["18-04-25", "Netflix", "Monthly", "199"],
#     ["18-04-25", "Spotify", "Monthly", "99"],
#     ["18-04-25", "Disney+", "Monthly", "149"],
#     ["18-04-25", "Amazon Prime", "Yearly", "999"],
# ]

# Add all entries
# for entry in entries:
#     DATA.append(entry)

# Calculate totals
subtotal = sum(int(entry[3]) for entry in entries)
discount = 0.05*subtotal
total = subtotal - discount

# Add total rows
DATA.append(["Sub Total", "", "", str(subtotal)])
DATA.append(["Discount", "", "", f"-{discount}"])
DATA.append(["Total", "", "", str(total)])

#determine indices of last 3 rows
last_row_index = len(DATA) - 1

# Create PDF
pdf = SimpleDocTemplate("receipt.pdf", pagesize=A4)
styles = getSampleStyleSheet()

title_style = styles["Heading1"]
title_style.alignment = 1
title = Paragraph("Bill", title_style)

# Table style
style = TableStyle(
    [
        ("BOX", (0, 0), (-1, -1), 1, colors.black),
        ("GRID", (0, 0), (-1, -1), 1, colors.black),
        ("BACKGROUND", (0, 0), (-1, 0), colors.HexColor("#2C3E50")),  # Header row background color
        ("TEXTCOLOR", (0, 0), (-1, 0), colors.white),  # Header text color
        ("ALIGN", (0, 0), (-1, -1), "CENTER"),
        ("BACKGROUND", (0, 1), (-1, -4), colors.HexColor("#F7F9FA")),  # Entry rows background color
        ("BACKGROUND", (0, -3), (-1, -3), colors.HexColor("#D6EAF8")),  # Subtotal row background color
        ("BACKGROUND", (0, -2), (-1, -2), colors.HexColor("#FDEBD0")),  # Discount row background color
        ("BACKGROUND", (0, -1), (-1, -1), colors.HexColor("#D5F5E3")),  # Total row background color
        ("FONTSIZE", (0, 0), (-1, -1), 12),
        ("BOTTOMPADDING", (0, 0), (-1, -1), 12),
        ("TOPPADDING", (0, 0), (-1, -1), 12),
    ]
)

table = Table(DATA, colWidths=[4*cm, 5*cm, 4*cm, 3*cm], style=style)

pdf.build([title, table])
