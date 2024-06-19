
SOURCE = $(shell find ../ -name '*.cpp')
PROG = main
OBJS = $(foreach src_o, $(SOURCE), $(basename $(notdir $(src_o))).o)
SUBDIR = $(eval seen :=) $(foreach src_n_dir,$(foreach src_dir, $(SOURCE), $(dir $(src_dir))),$(if $(filter $(src_n_dir),${seen}),,$(eval seen += $(src_n_dir)))) ${seen}
#compiler directives
CPP = g++
LIBS = -lpthread -lGL -lglfw3 -lGLEW -lpng 
INCLUDES = $(foreach src, $(SUBDIR), -I $(src))
CPPFLAGS = -g -pedantic $(LIBS) $(INCLUDES)
COUNTER = 1
#.SILENT
all: $(PROG)

$(PROG): $(OBJS)
	$(CPP) $(OBJS) -o $(PROG) $(CPPFLAGS)

$(OBJS): $(SOURCE)
	@echo $@
	@echo $(foreach src, $(SOURCE), $(if $(filter $(basename $@), $(basename $(notdir $(src)))), $(src)))
	$(CPP) $(CPPFLAGS) -c $(foreach src, $(SOURCE), $(if $(filter $(basename $@), $(basename $(notdir $(src)))), $(src))) -o $@
	

.cpp.o:
	$(CPP) $(CPPFLAGS) -c $^ -o $@

.PHONY: clean
clean:
	-rm -f $(PROG)
	-rm -f $(shell find ../ -name '*.o')

.PHONY: debug
debug:
	@echo $(INCLUDES)