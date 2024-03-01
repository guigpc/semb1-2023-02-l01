CC = arm-none-eabi-gcc
RM = rm -rf

OBJDIR = build
DEPDIR = .deps
SRCS = startup.c \
        main.c
CFLAGS = -g -mcpu=cortex-m4 -mthumb -Wall -O0 -I./inc
DEPFLAGS = -MMD -MP -MF $(DEPDIR)/$*.d

OBJS = $(patsubst %, $(OBJDIR)/%.o, $(basename $(SRCS)))
$(shell mkdir -p $(dir $(OBJS)) > /dev/null)

DEPS = $(patsubst %, $(DEPDIR)/%.d, $(basename $(SRCS)))
$(shell mkdir -p $(dir $(DEPS)) > /dev/null)

all: $(OBJS)

$(OBJDIR)/%.o: %.c $(DEPDIR)/%.d
	$(CC) -c $(CFLAGS) $(DEPFLAGS) $< -o $@
$(DEPS):
-include $(DEPS)

.PHONY: clean
clean:
	$(RM) $(OBJDIR) $(DEPDIR)


