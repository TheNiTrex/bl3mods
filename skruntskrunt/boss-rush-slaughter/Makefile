.PHONY: bk clean bpcharmod
MOD=boss_rush_3000.bl3hotfix
GEN=gen_boss_rush_3000.py
SEED=42
DISTFILES=$(MOD) boss_rush_3000.42.bl3hotfix.txt boss_rush_3000.666.bl3hotfix.txt boss_rush_3000.saurian.42.bl3hotifx.txt

mod: $(MOD)

clean: 
	rm -f 3000_simple.bl3hotfix gen_bpchars.json boss_rush_3000-42.bl3hotfix gen_bpchars.42.json

$(MOD): boss.py $(GEN)
	python3 $(GEN)

bk:
	cp boss_rush_3000.bl3hotfix "boss_rush_3000.bl3hotfix.$(shell date --iso=seconds)"

gen_bpchars.json: bpchar-gen.py boss.py
	python3 bpchar-gen.py --seed $(SEED)

bpcharmod: gen_bpchars.json $(GEN)
	python3 $(GEN) --json gen_bpchars.json --seed $(SEED) | fgrep Deploying | sort | uniq -c

# Seed 42
boss_rush_3000.42.bl3hotfix: bpchar-gen.py $(GEN)
	python3 bpchar-gen.py --json gen_bpchars.42.json --seed 42
	python3 $(GEN) --json gen_bpchars.42.json --seed 42 --output boss_rush_3000.42.bl3hotfix

# Pure random 
boss_rush_3000.rand.bl3hotfix: bpchar-gen.py $(GEN)
	python3 bpchar-gen.py --json gen_bpchars.rand.json 
	python3 $(GEN) --json gen_bpchars.rand.json --output boss_rush_3000.rand.bl3hotfix

# Seed any number
boss_rush_3000.%.bl3hotfix: bpchar-gen.py $(GEN)
	python3 bpchar-gen.py --json gen_bpchars.$*.json --seed $*
	python3 $(GEN) --json gen_bpchars.$*.json --seed $* --output boss_rush_3000.$*.bl3hotfix

# Rename to .txt
boss_rush_3000.%.bl3hotfix.txt: boss_rush_3000.%.bl3hotfix
	mv $< $@

dist: $(DISTFILES)

%.crash: %
	mv $< $@

# saurian theme
#
boss_rush_3000.saurian.42.bl3hotifx: bpchar-gen-saurian.py $(GEN)
	python3 bpchar-gen-saurian.py --json gen_bpchars_saurian.42.json --seed 42 --nomix
	python3 $(GEN) --json gen_bpchars_saurian.42.json --seed 42 --output boss_rush_3000.saurian.42.bl3hotifx

boss_rush_3000.saurian.%.bl3hotfix: bpchar-gen-saurian.py $(GEN)
	python3 bpchar-gen-saurian.py --json gen_bpchars_saurian.$*.json --seed $* --nomix
	python3 $(GEN) --json gen_bpchars_saurian.$*.json --seed $* --output boss_rush_3000.saurian.$*.bl3hotifx

boss_rush_3000.saurian.%.bl3hotifx.txt: boss_rush_3000.saurian.%.bl3hotifx
	mv $< $@
