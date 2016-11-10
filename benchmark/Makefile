URL = https://assets-cn.unigine.com/d/
VALLEY = Unigine_Valley-1.0
VALLEYBIN = $(VALLEY).run
HEAVEN = Unigine_Heaven-4.0
HEAVENBIN = $(HEAVEN).run

all:
	@echo "make [valley|heaven]"

valley:
	@[ -f $(VALLEYBIN) ] && echo "script $(VALLEYBIN) exist" || wget $(URL)$(VALLEYBIN)
	@[ -d $(VALLEY) ] && echo "directory $(VALLEY) exist" || sh $(VALLEYBIN)

heaven:
	@[ -f $(HEAVENBIN) ] && echo $(HEAVENBIN) exist || wget $(URL)$(HEAVENBIN)
	@[ -d $(HEAVEN) ] && echo "directory $(HEAVEN) exist" || sh $(HEAVENBIN)

clean:
	-rm -rf $(VALLEY) $(HEAVEN)
