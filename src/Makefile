#================================== COMPILER ==================================#
PROJECT_NAME = smartcalc
CC = gcc
#==============================================================================#


#=============================== DIRECTORY NAMES ==============================#
OBJ_DIR = ./obj
MODULES_DIR = ./modules
TEST_DIR = ./tests
REPORT_DIR = ./report
DVI_DIR = ./../docs
#==============================================================================#

#==================================== FLAGS ===================================#
# MAIN FLAGS FOR COMPILER
CFLAGS = -Wall -Werror -Wextra -pedantic -std=c11

GDB_FLAGS = -g -fsanitize=address -fsanitize=undefined -fno-sanitize-recover \
-fstack-protector -fanalyzer

# OPTIMIZATION
OPTIMIZE = -O0

# CHECK LIBRARIES FOR LINKING
LDFLAGS = -lcheck -lsubunit -lm

# CHECK & GCOV LIBRARIES FOR LINKING GCOV
LDGCOV = $(LDFLAGS) -lgcov

# FLAGS FOR COVERING MODULES
GCOV_FLAGS = -fprofile-arcs -ftest-coverage

# FLAGS FOR VALGRING TEST
VAL = --tool=memcheck --leak-check=yes

# FLAGS FOR CPPCHECK TEST
CPPCHECK = --enable=all --suppress=missingIncludeSystem
#==============================================================================#


#================================ TARGET NAMES ================================#
LIBRARY = $(PROJECT_NAME).a
TARGET = test
GCOV = gcov_report
#==============================================================================#


#================================ MAIN HEADER =================================#
MAIN_H = $(shell find ./ -maxdepth 1 -name "*.h")
#==============================================================================#


#====================== LIST OF FILE AND DIRS IN MODULES ======================#
MODULES_DIRS = $(shell find $(MODULES_DIR) -type d)
MODULES_C = $(shell find $(MODULES_DIR) -type f -name "*.c")
MODULES_H = $(shell find $(MODULES_DIR) -type f -name "*.h")
MODULES_O = $(notdir $(MODULES_C:%.c=%.o))
MODULES_OBJ_PATH = $(addprefix $(OBJ_DIR)/, $(MODULES_O))
#==============================================================================#


#==================== LIST OF FILE AND DIRS IN TEST MODULES ===================#
TEST_DIRS = $(shell find $(TEST_DIR) -type d)
TEST_C = $(shell find $(TEST_DIR) -type f -name "*.c")
TEST_H = $(shell find $(TEST_DIR) -type f -name "*.h")
TEST_O = $(notdir $(TEST_C:%.c=%.o))
TEST_OBJ_PATH = $(OBJ_DIR)/*_test.o
EXCLUDE = $(filter-out $(wildcard $(MODULES_DIR)/debug/*),$(MODULES_C))
#==============================================================================#


#================= LIST OF FILES TO CLANG-FORMAT AND CPPCHECK =================#
C_FILES = $(MODULES_C) $(TEST_C)
H_FILES = $(MODULES_H) $(MAIN_H) $(TEST_H)
ALL_FILES = $(C_FILES) $(H_FILES)
#==============================================================================#


#=============== CONFIGURING PATH TO SEARH FOR UNPREFIXED PATHS ===============#
vpath %.c $(MODULES_DIRS) : $(TEST_DIRS)
vpath %.o $(OBJ_DIR)
#==============================================================================#


################################################################################
#                      _                       _                               #
#                     | |                     | |                              #
#                    _| |_ __ _ _ __ __ _  ___| |_ ___                         #
#                   |_  __/ _` | '__/ _` |/ _ \ __/ __|                        #
#                     | || (_| | | | (_| |  __/ |_\__ \                        #
#                      \__\__,_|_|  \__, |\___|\__|___/                        #
#                                    __/ |                                     #
#                                   |___/                                      #
################################################################################


#================================= MAIN TARGETS ===============================#
all: $(TARGET) dvi

.PHONY: $(LIBRARY)
$(LIBRARY): $(OBJ_DIR) $(MODULES_O) $(MODULES_H) $(MAIN_H)
	ar rcs $@ $(MODULES_OBJ_PATH)
	ranlib $@

.PHONY: $(TARGET)
$(TARGET): $(LIBRARY) $(OBJ_DIR) $(TEST_O)
	$(CC) $(TEST_OBJ_PATH) $(LIBRARY) $(LDFLAGS) -o $@
	-./$@

$(GCOV): $(OBJ_DIR) $(REPORT_DIR) $(TEST_O)
	$(CC) $(TEST_OBJ_PATH) $(EXCLUDE) $(LDFLAGS) $(GCOV_FLAGS) -o $(addprefix $(OBJ_DIR)/, $(TARGET))
	-./$(addprefix $(OBJ_DIR)/, $(TARGET))
	gcovr -r . --html --html-details -o $(REPORT_DIR)/coverage.html
	xdg-open $(REPORT_DIR)/coverage.html

dvi:
	rm -rf $(DVI_DIR)
	doxygen Doxyfile
	xdg-open $(DVI_DIR)/html/index.html

clean:
	rm -rf $(OBJ_DIR)
	rm -rf $(REPORT_DIR)
	rm -rf $(DVI_DIR)
	rm -rf $(GCOV)
	rm -f $(TARGET)
	rm -f *.a *.o
	rm -f *.gc*
	rm -f main
	rm -f val.txt

rebuild: clean all
#==============================================================================#


#============================== CREATE DIRECTORIES ============================#
$(OBJ_DIR):
	mkdir -p ${OBJ_DIR}

$(REPORT_DIR):
	mkdir -p $(REPORT_DIR)
#==============================================================================#


#============================== OBJECTIVE TARGETS =============================#
%.o: %.c ${MODULES_H}
	$(CC) $(CFLAGS) $(OPTIMIZE) $(GDB_FLAGS) -c -o $(addprefix ${OBJ_DIR}/, $@) $<

%_test.o: %_test.c ${TEST_H} ${MAIN_H}
	$(CC) $(CFLAGS) -c -o $(addprefix ${OBJ_DIR}/, $@) $<
#==============================================================================#


#=============================== CHECKS TARGETS ===============================#
clang_check:
	clang-format -style=Google -n -Werror $(ALL_FILES)

clang_fix:
	clang-format -style=Google -i $(ALL_FILES)

cppcheck:
	$@ $(CPPCHECK) $(MODULES_C) $(MODULES_H)

valgrind: $(TARGET)
	@printf '\033[1;33m\n\t\t\t\t                   _            _           _   _            _   _             \n'
	@printf '\t\t\t\t                  | |          (_)         | | | |          | | (_)            \n'
	@printf '\t\t\t\t       __   ____ _| | __ _ _ __ _ _ __   __| | | |_ ___  ___| |_ _ _ __   __ _ \n'
	@printf '\t\t\t\t       \ \ / / _` | |/ _` | '\''__| | '\''_ \ / _` | | __/ _ \/ __| __| | '\''_ \ / _` |\n'
	@printf '\t\t\t\t        \ V / (_| | | (_| | |  | | | | | (_| | | ||  __/\__ \ |_| | | | | (_| |\n'
	@printf '\t\t\t\t         \_/ \__,_|_|\__, |_|  |_|_| |_|\__,_|  \__\___||___/\__|_|_| |_|\__, |\n'
	@printf '\t\t\t\t                      __/ |                                               __/ |\n'
	@printf '\t\t\t\t                     |___/                                               |___/ \n\033[0m\n'

	@$@ $(VAL) ./$(TARGET) > val.txt 2>&1 && \
	{ \
		printf "\033[1;33m\n"; \
		printf "###########################################################################################################################################################\n\n"; \
		printf "                                                                 Valgrind test results:\n"; \
		printf "                                                             Passed tests $$(grep "ERROR SUMMARY: 0" -c val.txt) from $$(grep "ERROR SUMMARY:" -c val.txt)\n\n"; \
		printf "###########################################################################################################################################################\n"; \
		printf "\033[0m\n"; \
	}
#==============================================================================#


#============================= ADDITIONAL TARGETS =============================#
dependencies:
	sudo apt install cppcheck
	sudo apt install clang-format
	sudo apt-get install check
	sudo apt install doxygen
	sudo apt-get install graphviz
	sudo apt-get install texlive
#==============================================================================#
