# assignments
import sqlite3
import argparse

# Setup for CLI. Do not touch!
# ===== BEGIN CLI BLOCK ===== # 

slab = sqlite3.connect(chinook.db) 


c = slab.cursor()

c.execute(INSERT INTO Tracks (name)
VALUES('Like Ships'))

c.execute(SELECT
	TrackId,
	Name
FROM
	Tracks
ORDER BY
	TrackId DESC
LIMIT 1;) 
c.execute(
);) 

c.execute("INSERT INTO Like Ships VALUES ('Soundtrack for the show Over the Garden Wall','makes me feel like I'm eating a pb & j sandwhich watching paper boats float down a creak')")
slab.commit()
slab.close()
parser = argparse.ArgumentParser()
parser.add_argument("db", default=":memory:", help="The file path of the database to be edited")
parser.add_argument("-r", "--roster", help="Inserts names from ROSTER into db. ROSTER should be a plain-text file with one name on each line.")
args = parser.parse_args()

# ===== END CLI BLOCK ===== #

conn = sqlite3.connect(args.db)
cur = conn.cursor()

if args.roster:
    with open(args.roster) as f:
        for record in f:
            name = record.strip()
            cur.executescript(f"INSERT INTO students (name) values ('{name}')")
            conn.commit()
        conn.close()

else:
    while True:
        name = input("Type your first and last name and hit enter to register. Hit Ctrl+C to quit.\n> ")
        cur.execute(f"INSERT INTO students (name) VALUES ('{name}');")
        conn.commit()
